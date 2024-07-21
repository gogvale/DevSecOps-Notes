## Spider

The first tool we used is the spider - which from a starting point in the application looks for `<a>` tags and adds to the project recursively (the only problem with that is when pages are added dynamically using js, like in modern frameworks).

We can access it on **Tools -> Spider**

## AJAX Spider
To overcome this issue we can repeat the process using another tool that opens a sandbox browser and follow links after they're added to the DOM (using a headless browser might improve the performance a little)

We can access it on **Tools -> AJAX Spider**
## Tailoring scope
Sometimes we don't want to look for every possible vulnerability in a project. If a site doesn't have a database a SQL Injection will not work, so it can be safely skipped.

We can modify the scanning policies on **Analyse -> Scan Policy Manager** 

On each item there are 2 configurations available: **Threshold** and **Strenght**.
* Threshold refers to the verbosity - higher mean that it will only report if it's absolutely sure is correct
* Strength controls how many tests are run for each category - higher will report additional findings, but might take longer

## Active scanning

**Active scanning** in ZAP simulates attacks on a web application to identify potential security vulnerabilities. It works by sending various malicious requests to the application and analyzing the responses for signs of weakness. These requests are based on known attack techniques that hackers might exploit. Additionally, we can add the scope from the previous step in the policy input.

We can access it on **Tools -> Active Scan**
After the scan finishes, the results are added to the **Alerts** tab at the bottom.

## Authentication
When dealing with authentication based attacks, we can achieve it by adding a script to authenticate by mimicking the browser and sets of rules to check if the user is authenticated (as well as removing links from the scope that might log us out, since the attacks run sequentially).

### Scripting
1. Disable the ZAP HUD from the toolbar
2. Select **Record a New ZEST Script** button on the toolbar (tape icon)
3. On the dialogue, set:
	1. type to **Authentication**
	2. record type to **Server side script**
	3. prefix to starting url (in this case, the home page)
4. Select the start recording  button and then the browser icon
5. Proceed with login steps
6. Stop recording by clicking the **Record a New ZEST Script** button again and close browser
7. On the scripts tab besides sites (left part of the screen) delete unnecessary requests
8. Select the script and on **Script console** select **Run** to make sure it works as expected
### Context
Now that we created an authentication script we must add it to our scope before running a scan:
![[Pasted image 20240717190549.png]]
![[Pasted image 20240717190606.png]]


> [!Important] 
> Be sure to click the **Load** button to the right of the script's name


> [!Important]
> To do authenticated scans, ZAP will also need you to define at least one user in the **Users** section. This won't be used at all in our case, as our ZEST script embeds the user and password we'll use. However, ZAP needs a user to be defined, or it will just skip authentication altogether
> 
> ![[Pasted image 20240717190807.png]]


### Avoiding logouts

To prevent ZAP from logging itself out, we will right-click the logout.php script in the Sites tab and exclude the script from our context:
 
 ![[Pasted image 20240717190932.png]]
### Detecting if logged in
We might check the current session state by querying a known page and adding flags:

![[Pasted image 20240717191157.png]]
**Flag as Context -> (Your Context Name): Authentication Logged-in indicator:**


![[Pasted image 20240717191209.png]]
**Flag as Context -> (Your Context Name): Authentication Logged-out indicator.**

Then we need to choose a Verification Strategy to tell it how to use the configured patterns correctly. In this case, we will use the Poll the Specified URL strategy and tell it to poll the `/aboutme.php` resource every 60 requests to check for the logged-in/logged-out patterns.
To do this, double-click the Context and change the following settings under **Authentication**:

![[Pasted image 20240717191427.png]]

## Checking APIs
ZAP can import APIs defined by **OpenAPI** (formerly **Swagger**), **SOAP** or **GraphQL**.
ZAP supports two methods to import API definitions: you can provide an offline file or a URL from where to download them. 
Go to **Import -> Import an OpenAPI definition from a URL**. Specify the corresponding URL and hit the **Import** button.

![[Pasted image 20240717191650.png]]
After that proceed with attack as usual:
![[Pasted image 20240717191714.png]]

## Running Automated Scans With zap2docker

To integrate ZAP in our pipeline, we will use **zap2docker**, a dockerized version of ZAP proxy built with automation as its primary purpose. The full documentation for zap2docker can be found [here](https://www.zaproxy.org/docs/docker/).

**Note:** The commands in this section are provided for reference only. You don't need to run them manually, as we will have Jenkins do it for us later.

To install zap2docker, you can pull it from Docker Hub using the following command:

```none
docker pull owasp/zap2docker-stable
```

### Scan profiles:  

#### Baseline Scan
ZAP will spider the target website for a maximum time of 1 minute. No active scan will be performed. You can optionally run an AJAX spider if desired.

```none
docker run -t owasp/zap2docker-stable zap-baseline.py -t https://www.example.com
```

#### Full Scan
ZAP will run a spider with no time limits, followed by an active scan.

```none
docker run -t owasp/zap2docker-stable zap-full-scan.py -t https://www.example.com
```

#### API Scan
ZAP will perform an active scan against an API. You will need to provide a URL to an API description file (OpenAPI, GraphQL or SOAP).  

```none
docker run -t owasp/zap2docker-stable zap-api-scan.py -t https://www.example.com/swagger.json -f openapi
```


> [!NOTE] 
> In any of the scans, the results for passive scans will be limited to 10 alerts. In addition to the base commands, you can add the `-j` switch to perform an AJAX scan on the baseline and full scans.

