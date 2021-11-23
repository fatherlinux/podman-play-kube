# Kube Play Demo
WIth Podman 3.4 and above, we've added a couple of new features that really make Kubernetes YAML a reasonable alternative to Docker Compose. Both of these features are part of the ```podman play kube``` subcommand, and they could have easily been overlooked if you weren't paying attention. I believe these latest features really push Kubernetes YAML to a tipping point where it's usable everywhere. With these features, you can use it for local development in Podman, as well as production deployments on a Kubernetes cluster (like OpenShift). In my mind, this is the holy grail. Now, we have a standardized image format, as well as a standardized deployment format. This demo will highlight both fo these features working together in a simple workflow which a developer might use.

The first feature enables podman to automatically build a container image when it's referenced in the Kubernetes YAML, but not found in the local container image cache. In the Podman 3.4 release, it's described like this:

* The podman play kube command now supports building images. If the --build option is given and a directory with the name of the specified image exists in the current working directory and contains a valid Containerfile or Dockerfile, the image will be built and used for the container.

The next feature is the ability to tear down an set of resources. Podman will tear down anything defined in the Kubernetes YAML file and essentially clear out your enviornment similar to a ```compose down``` command. The feature is described in the Podman 3.4 release notes like this:

* The podman play kube command now supports a new option, --down, which removes any pods and containers created by the given Kubernetes YAML.

Next, let's get to the demo. First clone this GitHub repository:

```git clone https://github.com/fatherlinux/podman-play-kube```

Next, just bring up the environment with Podman 3.4 or newer:

```cd podman-play-kube```

```podman play kube ubi-httpd.yaml```

Test that the pod is running:

```curl localhost:8080```

When you are done testing, bring the environment back down:

```podman play kube --down ubi-httpd.haml```

Clear out the environment:

```podman pod kill -a```

```podman pod rm -a``` 

It's that easy. A single command to bring up an environment, and a single command to tear it down. This demo is simple and shows a single pod, but this workflow could be used to develop more complex applications with two, three or 10 pods working in conjunction. In fact, I plan on using this for a side project I am working on where I need Rails, Postgres and Redis all running side by side for an application. More to come soon! 
