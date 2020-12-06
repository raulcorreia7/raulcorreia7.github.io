# Installing Docker in Ubuntu 20.10 (Groovy Gorilla)


## Ubuntu ❤️ Docker
Hello everyone,

Recently I installed the latest non LTS version of [Ubuntu 20.10 Groovy Gorilla](https://releases.ubuntu.com/20.10/), and found it a bit of a hassle to install Docker with [this](https://docs.docker.com/engine/install/ubuntu/), following the repository tutorial step.

<!--more-->


### Analysis of the problem 🔎
So, analyzing the tutorial I found a problem on the 3rd point on through the **SET UP THE REPOSITORY** step.

{{< highlight bash >}}
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
{{< /highlight >}}

### Error ⛔
The error is in:

{{< highlight bash >}}
    "..
    $(lsb_release -cs) \
    stable"
{{< /highlight >}}

This expands to **groovy stable**, and ___at the time of writing___ and from my analysis, it is not supported by the stable docker community repositories.

### The fix ✅

So the workaround is simply to use a the **test** branch of the repository. 

{{< highlight bash >}}
    "..
    $(lsb_release -cs) \
    test"
{{< /highlight >}}


{{< admonition type=info title="Info" open=true >}}

I believe if you are using a **non-LTS** version of Ubuntu, you want fresher or nearer rolling-release software update, so using this repository shouldn't be a issue. I'm not responsible for any faults, errors or breaks.

{{< /admonition >}}

### Automated Script 🔨
So I came up with a simple script to setup and automate everything for you.

{{< admonition type=warning title="Warning" open=true >}}

This is fully automated, there is no end user confirmation whatsoever.

{{< /admonition >}}


{{< highlight bash >}}

#Install needed dependencies
sudo apt install apt-transport-https \
         ca-certificates \
         curl \
         software-properties-common \
         -y 
#Download the docker repository gpg key and add it.
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu groovy test" -y
#Install everything related to docker
sudo apt install docker-ce docker-ce docker-ce-cli containerd.io -y
{{< /highlight >}}


[Here](https://github.com/raulcorreia7/scripts/blob/master/ubuntu/install-docker.sh) is the latest version of the script on my GitHub.

King regards,

Raúl 🐧
