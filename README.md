# Kube Play Demo
This demo makes it super easy to test out the new Podman Play functionality which makes it a lot more like Docker Compose. First check out this demo:

```git clone https://github.com/fatherlinux/podman-play-kube```

Now, just bring up the environment with Podman 3.4 or newer:

```cd podman-play-kube```
```podman play kube ubi-httpd.yaml```

Test that the pod is running:

```curl localhost:8080```

When you are done testing, bring the environment back down:

```podman play kube --down ubi-httpd.haml```

Clear out the environment:

```podman pod kill -a```
```podman pod rm -a``` 
