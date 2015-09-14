# dspace-cocoon-sitemap-impl

This is a patched version of cocoon-sitemap-impl which resolves an issue with Cocoon being too noisy about 404 errors (see https://jira.duraspace.org/browse/DS-2748).

## Building the jar

After cloning this repository, run the following to build the jar in the target/ directory.

    mvn package

## Applying to DSpace

If you're using a DSpace version that doesn't incorporate the PR[1] for DS-2748 yet, you can still use this patch by doing the following:

* Stop DSpace
* Find the deployed xmlui webapp's WEB-INF/lib/ directory and remove the cocoon-sitemap-impl-1.0.0.jar file from it.
* Put the built dspace-cocoon-sitemap-impl-1.0.0.jar in this directory instead.
* Restart DSpace

The Cocoon log should now start showing 404s as WARNings instead of ERRORs, and without stack traces.

Note that the request URI won't appear in the message unless DSpace is also patched as per the PR below.

[1] This pull request incorporates this patched jar into the DSpace build and updates DSpace to include the sitemap URI in the logged messages:
https://github.com/DSpace/DSpace/pull/1054
