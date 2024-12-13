# Learn Kubernetes the kind way	

[TOC]

Local [Kubernete](https://kubernetes.io/) exercise for documenting and playing with [Helm](https://helm.sh/) locally.

The purpose of this repo is to share some fantastic tools for playing with Kubernetes and Helm. I feel as a full stack developer that I don't get an excuse to play with this enough, to understand it like a devops engineer does. Recently that all changed as I had a reason to do this for setting up a local development project with lots  of scaled out microservices using scaling or *replicas*. My local environment was a docker setup and it only scaled to one solitary instance and possibly a manual second outside of docker. 

So I discussed this with my lovely colleague, *Aditya Gundecha*, and he shared some lovely tools with all of us that I feel are a must have for any team wanting to get their hands dirty with Kubernetes locally, and other *devopsy* things. So this is a dedication to *Aditya*, who shared with me and now I want to pass on this with others in the open source spirit of learning.

I have a Mac, but I am 99% sure everything works on other platforms, follow the links ...

## Tools

![Kube tools](assets/kubetools.png)

1. [kind](https://sigs.k8s.io/kind) is a tool for running local Kubernetes clusters using Docker container “nodes”.
   kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

   ```bash
   ❯ brew install kind
   ```

2. If you have [go](https://golang.org/) 1.16+ and [docker](https://www.docker.com/), [podman](https://podman.io/) or [nerdctl](https://github.com/containerd/nerdctl) installer. I used docker for this.

3. Install [helm](https://helm.sh/) and learn lots from this site

   ```bash
   ❯ brew install helm
   ```

4. Learn about [Argo-cd](https://argo-cd.readthedocs.io/en/stable/getting_started/) for Kubernetes and git repositories and become a legend.

5. [Dotfiles](https://dotfiles.github.io/) is a devops helper site for programs that help with managing, syncing, and/or installing your dotfiles which ***Backup\***, ***restore\***, and ***sync\*** the prefs and settings for your toolbox. 

6. [K9s](https://k9scli.io/) is a terminal based UI to interact with your Kubernetes clusters. The aim of this project is to make it easier to navigate, observe and manage your deployed applications in the wild. K9s continually watches Kubernetes for changes and offers subsequent commands to interact with your observed resources.

   ```bash
   ❯ brew install derailed/k9s/k9s
   ```

   ![k9 terminal in vscode](assets/k9-terminal.png)

7. [Backstage](https://backstage.io/demos/) is an open source framework for building developer portals from *Spotify*.

8. https://github.com/jesseduffield/lazygit speaks for itself.

9. [tmux](https://github.com/tmux/tmux/wiki) is a terminal multiplexer. It lets you switch easily between several programs in one terminal, detach them (they keep running in the background) and reattach them to a different terminal.  

## Exercises

### Setup kind to run nginx

The purpose of this exercise is to learn how to setup and use **kind** to generate a local kubernete stack. For more information see more [here](learn-kind.md).

### 1. Setup a Mongo on kind

The purpose of this is to setup [Mongo](https://www.mongodb.com/blog/post/top-4-reasons-to-use-mongodb-8-0?tck=mdb80_blog_pencil_banner) and [Mongo Express](https://www.mongodb.com/resources/products/compatibilities/express) on here for database usage going forward, to get it wrong and to debug how to get it right ... using everything learnt in the first exercise. For more information see more [here](learn-mongo.md).

### 2. Setup Helm and helloworld on Argocd

The purpose of this is to learn and use helm with a deployment tool to understand how helm works and how you can deploy an app to this space. For more information read [here](helm-argocd-helloworld.md).

### 3. Setup a mock digital commerce platform

The purpose of this is to be able to link up with an existing docker image and get it deployed to Argo. So this assumes you have setup the previous exercise, ready to use Helm and Argo. For more information read here.

- Create **fabric, inventory and search** using helm as placeholders to get deployed to argo

```bash
❯ helm create Fabric

Creating Fabric

❯ helm create Inventory

Creating Inventory

❯ helm create Search

Creating Search
```

## References

TODO
