sudo su && git clone && import requests
import json

TOKEN = '<YOUR-TOKEN>'
OWNER = '<OWNER>'
REPO = '<REPO>'
API_VERSION = '2022-11-28'
HEADERS = {
    'Authorization': f'Bearer {TOKEN}',
    'Accept': 'application/vnd.github+json',
    'X-GitHub-Api-Version': API_VERSION
}

# Create a Blob
data = {
    'content': 'Hello, GitHub blob!',
    'encoding': 'utf-8'
}
response = requests.post(
    f'https://api.github.com/repos/{OWNER}/{REPO}/git/blobs',
    headers=HEADERS,
    data=json.dumps(data)
)
print(response.json())

# Get the blob SHA from the response
sha = response.json().get('sha')

# Retrieve a Blob
if sha:
    response = requests.get(
        f'https://api.github.com/repos/{OWNER}/{REPO}/git/blobs/{sha}',
        headers=HEADERS
    )
    print(response.json())Exposes `gh` to the global environment. Tries to follow both the form of Github
HTTP API and JS style.

```js
gh.authenticate("fitzgen", "sdfk32we-FAKE-uydfs7f-rhrwe8r7");
var huddlej = gh.user("huddlej");
huddlej.show(function (data) {
    console.log(data.user);
});
huddlej.repos(function (data) {
    console.log("Number of repos: " + data.repositories.length);
});
var wujs = gh.repo("fitzgen", "wu.js")
wujs.show(function (data) {
    console.log("Number of watchers: " + data.repository.watchers);
});
wujs.update({ has_wiki: 0 }); // Unfortunately, no callbacks with POSTs :(
```

COMPLETE
========

* Authentication
* Users
* Repos
* Commits
* Issues
* Gists
* Network
* Objects

TODO
====

* Documentation
