# Helm repo and https

This URL:

```shell
https://artifactory.mycooldomain.com/artifactory
```

Is different from this URL:

```shell
https://artifactory.mycooldomain.com:433/artifactory
```

Here's the deal, with the `:443` URL you can authenticate and even scrape the index.  However, you cannot pull
down an archive fromt he repo.

Apparently the `:443` has some weird impact on downloads of archives.  The result will be a 401 when trying to 
install a chart.

However, you won't get the same 401 when updating or authenticating to the repository.

Weird, right?  This was not a fun thing to discover.
