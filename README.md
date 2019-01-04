# 3scale-secure-github-api
Simple demonstration using 3Scale to secure https://api.github.com:443

## Create the Service
1. Show the API to secure on https://api.github.com
2. We will secure 2 endpoints :
	1. user_url
	2. user_repositories_url
3.  Create the API (Service) 
	1. Name : Github API
	2. System Name : github
4. Create 2 application plans : silver & gold
5. Publish both application plans and set default plan as Silver

## Create the consumer (application)
7. Go to Audience -> Listing, select the account Developer
8. Click on Applications on top and then click on create application

## Configure the API Gateway Integration
1. Go to API : Github API
2. Integration -> Configuration -> Edit configuration
3. Set private URL to https://api.github.com:443
4. In Authentication Settings, set Credentials location as HTTP Headers
5. Left API test GET request to /
6. Click button Update & test in Staging Environment. The bar on the left should be green in order to validate the integration
7. Verify with curl 
```bash
curl "https://api-2445582632153.staging.gw.apicast.io:443/" -H 'user_key: c87ffb1ddde74f4cd7f6750d0113bffd' | jq .
```
7. Show that the authentication failed if you don’t  have the right API key

## Analytics
1. Go to API: Github API -> Integration -> Methods & Metrics
2. Click on `New Method`, and add method for get user
	1. Method name: Get user
	2. System Name : get_user
3.  Click on `New Method`, and add method for get metadata
	1. Method name: Get Metadata
	2. System Name : get_metadata
4. Click on `New Method`, and add method for get repos
	1. Method name: Get User Repos
	2. System Name : get_user_repos

### Add the mapping rules
1. Realize some hits on each endpoints
2. Go to Analytics -> Usage

## ActiveDocs
1. Go to ActiveDocs -> Create your first spec
	1. Name : Github
	2. System name : github
	3. Tick the box `Publish?`
	4. Import JSON API spec from https://xch.app.itix.fr/3scale-training/github.json
		1. Remember to change the gateway hostname
	5. Go to the developer portal and log in as a user from the Developer Account
	6. Try the API through ActiveDocs

## Extension for the demonstration
1. Messaging between consumers and producers
2. Rate limiting
3. Audience and manager of partners community
4. Self-service through Developer Portal. Create your application, choose a plan and consume the API
