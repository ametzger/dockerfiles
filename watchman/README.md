# ametzger/watchman

Utility image of
[facebook/watchman](https://github.com/facebook/watchman) built using
a base image binary-compatible with official `python` images.

## Usage

In your `Dockerfile`, add the following lines:

``` dockerfile
COPY --from=ametzger/watchman /usr/local/bin/watchman* /usr/local/bin
RUN mkdir /usr/local/var/run/watchman \
    && chown -R /
```

Note: you may need to alter the permissions of
`/usr/local/var/run/watchman` to match any USER directives.
