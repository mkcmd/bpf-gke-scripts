# bpf-gke-scripts
scripts 4 ez k8s bpf agent fun

## Getting started

First you need to have gcloud SDK
[installed](https://cloud.google.com/sdk/docs/install), as well as `kubectl`.

Then when you authenticate do set a defalt project id and zone, otherwise run
these default configs:

```
gcloud config set project cmd-dev-1
gcloud config set compute/zone us-east1-b
```

## Actually running the script

The whole point of these scripts are for ez swapping out of custom agent builds
-- maybe you want it to have symbols for a debugger or for it to actually log
stuff. First thing you need to do is drop your packaged agent in here:

```
cp <path to ma boi>.deb daemonset/
```

Then make sure to modify the `daemonset/cmd_config.yaml` to contain your
backend info like the project key, now all you gotta do is run `init` with a
name of your cluster:

```
./init i-like-the-stock
```

the script will build, tag, push the docker image for you, and set up all
the annoying apparmor stuff that neither of us cares about.

Now you'll have a cluster running with the bpf agent running on all the nodes.
Go have fun kid, just remember that to clean it all up you run:

```
./deinit
```
