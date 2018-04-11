# Custom compilation of Openshift origin-web-console

## Compilation

1. Build project

   ```
   # in origin-web-console repo dir
   make build
   ```

1. Commit changes
1. Clone `origin-web-console-server` to a proper location. Typically it's `~/go/src/github.com/openshift/origin-web-console-server`

   ```
   go get github.com/openshift/origin-web-console-server
   ```

1. Select branch matching to branch used in `origin-web-console` project.

   ```
   # in origin-web-console-server repo dir
   git branch <branch-name>
   ```

1. Vendor origin-web-console files

   ```
   GIT_REF=<origin-web-console commit reference> CONSOLE_REPO_PATH=<path to origin-web-console repo dir> make vendor-console
   ```

1. Create the image

   ```
   OS_BUILD_ENV_PRESERVE=_output/local/bin hack/env make build-images
   ```

   New image is available in local docker registry as `openshift/origin-web-console:latest`.
   
### Cross-compilation of `console`, `catalog` and `common`

Described in official [README](https://github.com/openshift/origin-web-console/tree/6e1128d11def43550570593a46c700fd43c2f645#contributing-to-the-primary-repositories).

## Deployment

1. Let's have a cluster running. E.g. `oc cluster up`.
1. Change image in deployment specification:

   ```
   oc login -u system:admin
   oc patch deployment/webconsole --patch '{ "spec": { "template": { "spec": { "containers": [ { "name": "webconsole", "image": "openshift/origin-web-console:latest" } ] } } } }' -n openshift-web-console
   ```
