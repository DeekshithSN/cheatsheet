## How to Install Kubernetes on Mac

This is a step-by-step guide to installing and running Kubernetes on your Mac so that you can develop applications locally.

You will be guided through running and accessing a Kubernetes cluster on your local machine using the following tools:

### Homebrew
### Docker for Mac
### Minikube
### virtualbox
### kubectl
### Installation Guide

- The only pre-requisite for this guide is that you have Homebrew installed. Homebrew is a package manager for the Mac. You’ll also need Homebrew Cask, which you can install after Homebrew by running brew tap caskroom/cask in your Terminal.

- Install Docker for Mac. Docker is used to create, manage, and run our containers. It lets us construct containers that will run in Kubernetes Pods.

- Install VirtualBox for Mac using Homebrew. Run brew cask install virtualbox in your Terminal. VirtualBox lets you run virtual machines on your Mac (like running Windows inside macOS, except for a Kubernetes cluster.)

Skip to step three if everything has worked to this point.

In my case, I already had the non-Homebrew VirtualBox app installed which caused issues when trying to start minikube.

If you already have VirtualBox installed, start the installation as before with brew cask install virtualbox. You will get a warning that confirms this saying Warning: Cask 'virtualbox' is already installed.. Once this is confirmed, you can reinstall VirtualBox with Homebrew by running brew cask reinstall virtualbox.

If you happen to have VirtualBox already running when you do this, you could see an error saying Failed to unload org.virtualbox.kext.VBoxDrv - (libkern/kext) kext is in use or retained (cannot unload).

This is because the kernel extensions that VirtualBox uses were in use when the uninstall occurred. If you scroll up in the output of that command, beneath Warning! Found the following active VirtualBox processes: you’ll see a list of the processes that need to be killed.

Kill each of these in turn by running kill first_column_number (first_column_number is the process identifier for that process).

Now re-run brew cask reinstall virtualbox and it should succeed.

- Install kubectl for Mac. This is the command-line interface that lets you interact with Kuberentes. Run brew install kubectl in your Terminal.

- Install Minikube via the Installation > OSX instructions from the latest release. At the time of writing, this meant running the following command in Terminal…

curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.27.0/minikube-darwin-amd64 &&\
      chmod +x minikube &&\
      sudo mv minikube /usr/local/bin/
Minikube will run a Kubernetes cluster with a single node.

Everything should work! Start your Minikube cluster with minikube start. Then run kubectl api-versions. If you see a list of versions, everything’s working! minikube start might take a few minutes.

At this point, I got an error saying Error starting host: Error getting state for host: machine does not exist. because I had previously tried to run Minikube. You can fix this by running open ~/.minikube/ to open Minikube’s data files, and then deleting and deleting the machines directory. Then run minikube start again.

