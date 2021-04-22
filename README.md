# Template for deploying a Shiny app with Docker

In this repository you can find the code to run a R shiny app with docker. In the first part of this README you will find instructions to do it. In the second part you can find instructinos to run it in AWS.

Any doubts or corrections, open an issue or send me a mail to ge.vargasn@gmail.com

### Running a shiny with Docker

I assume you have installed [docker](https://www.docker.com/products/docker-desktop) on your pc. It would be enough with having the docker engine, but installing the default Docker Deskop is also good, as it has the other one inside.

Clone this repository in some location on your pc. Open the terminal and go to the `shiny_docker_exampple` you just cloned. With the next command you will build the image from the Dockerfile (if you are using Windows, just remove the `sudo`):

```
# don't forget the point!
sudo docker build -t shiny_image .
```

With this you have created two imagens: `shiny_image` and `rocker/shiny`. Let's run `shiny_image` in a container named `shiny_app` with the next command (again, if you are in windows, don't use the `sudo`):

```
sudo docker run --name=shiny_app --rm -p 80:3838 shiny_image
```

Now, if you go to [http://0.0.0.0/](http://0.0.0.0/) we can see that the app is running.




### Running a shiny with docker in AWS

Launch an instance in the cloud. I have used AWS Ubuntu Server 20.04 LTS/64 bits (x86)/t2.micro and the next options for the `Edit security group`:

<img src="aws_inbound_rules_shiny.png" alt="Rules for AWS Shiny app" width="600"/>

Connect your terminal with the instance. In AWS the easiest way is using a pem file. You should see something like this:

<img src="terminal_connected.png" alt="Terminal connected to AWS" width="600"/>

You already has git installed (you can check writing `git` on the console). Now, install docker using [the commands from its web](https://docs.docker.com/engine/install/ubuntu/). Probably they will be like these:

```
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

To check if all is correct, try `sudo docker run hello-world`.

Now, just clone this repository and use the commands from the first part of the readme. 

```
git clone https://github.com/gustavovargas/example_shiny_docker.git
cd example_shiny_docker
sudo docker build -t shiny_image .
sudo docker run --name=shiny_app --rm -p 80:3838 shiny_image
```

Just realise that your app is running in the http direction, like for example `http://3.15.188.202/`, not the https. If you want to enable the https, just follow [this instructions](https://support.rstudio.com/hc/en-us/articles/213733868-Running-Shiny-Server-with-a-Proxy)