# My documentation

My computer specifications that im doing the assignment with:

OS: Windows 10 Home

Processor: Intel(R) Core(TM) i7-4770K CPU @ 3.50GHz

GPU: GeForce GTX 1080

RAM: 16 gt

Ancient "gaming" PC that can shut off or freeze at any moment and works in mysterious ways.

# Getting started

Having none of the required software installed I had to start with that. First I wrote docker for windows into search and clicked the first link and installed it. Unable to start Docker I had to enable virtualization in my BIOS settings. I restarted computer, pressed DEL and entered BIOS settings. There I enabled Intel virtualization and saved settings. Restarting my computer I was still unable to access Docker because I was missing virtualization software so I had to install something for that. I chose VirtualBox since I have previous experience with that. Googled VirtualBox, clicked downloads and there Windows hosts and it installed it. Next it complained about Linux kernel not being up to date so I googled the problem and opened cmd.exe as admin and entered: wsl --update after which it updated my kernel. Now my Docker was able to start and I made an account for it.

Next up I decided to continue my work with this thing aka GitHub since I intend to return my work here. Logged into my old account and made weatherapp repo. I downloaded git bash for Windows since I figured it would be easier to use with their own commandline. After messing with the installing options and choosing the ones I like it started to install. My computer being the mess it is I decided to clone the assignments repo to my downloads folder. I went into the folder and right clicked open GIT Bash here. I went into the assignments repo, clicked code and there the https clone link. 

![image](https://github.com/aexceed/weatherapp/assets/129611461/f9bfe07c-dee6-4f0d-88c1-a51cc475ab5d)

Entered command $ git clone https://github.com/eficode/weatherapp.git to get the files to my computer. Next up I wanted to put the repo into my own github so It´s there and ready to be returned. Enter command $ git remote rename origin upstream to remove the link to the original repo and $ git remote add origin https://github.com/aexceed/weatherapp.git to add mine as the future reference. Now I want to push it to my repo to see if it´s there and make my life easier being able to see the whole thing. Change it from master to main, enter command: $ git branch -m main and to push it to my repo: $ git push -u origin main. It wanted my account credentials which I gave but error came up.

![image](https://github.com/aexceed/weatherapp/assets/129611461/17970164-4362-4697-9fc1-ba0f0b6d1ef4)

Something about support for password authentication being removed so now I needed to figure workaround for it. Little bit of googling and I found out you can make personal access token to use instead of password and then it will work. Click Account -> settings -> Developer settings -> Personal access tokens. I chose fine grained token, gave it some name and in permissions I gave it permission to push to repo. Enter the command again and now in password screen I copied the token key and it worked pushing repo from my computer to GitHub.

There was also something about needing API key so i went to the openweathermap website and tried to create account but found out I already had one. Interesting since I don´t remember having one. Well after recovering my account I went to look and I had active API key which I will use in this. I went into weatherapp files in backend folder, there in src folder I found index.js file that felt like the place to put my API key in. I put my API key here like the syntax on weathermap side showed:

![image](https://github.com/aexceed/weatherapp/assets/129611461/c664d1e7-546c-4500-8724-265dcd588ca2)


# Docker

Since I had no previous experience of using Docker I decided to do few simple tasks that it was recommending on the desktop clients page. After doing a couple of them I got the idea of the software but it didnt´t really give me anything on where to start building Dockerfile. I googled docker compose and hot reloading and realized I first need to get my regular Dockerfiles working before I can even think about those. I fell down rabbit hole with my Dockerfile searches with no real progress a couple hours later so I decided to take a little break. 

Trying to get the whole thing working instantly instead of putting smaller parts together I started frontend Dockerfile first. I tried a few iterations but got kind of lost in the sauce and forgot to document them, my bad there. I got the dockerfile and container started but then when it didn´t show anything in browser I thought maybe I need some kind of web server. I chose nginx and continued work with dockerfile.  Installed nginx extension to my docker and made Dockerfile based on ideas from internet. Had some trouble getting it to work but then I added script to package.json file and it started doing something. For some reason my page only showed the basic nginx page instead of that file I was given. Tried to get it to work but it was hopeless. Thought came to my mind that maybe I needed to do react part of the tasks to have it really working so I just left it like that. I got my container to start and show something that´s gotta count for something right? You can read more of my thoughts (if there was any sense in them) about that one inside the Dockerfile comments. 

Now for the backend I chose same alpine but yarn instead of npm for package manager, this one was pretty simple compared to frontend in my mind. Some googled parts of code and it ran pretty much straight away. I also found out about .dockerignore file to hide some of the files that are unneccessary and take less space for Docker image so I added it and couple lines in there that seemed to be best practices. Starting the container and checking if the port shows anything and nothing showed up. I´ll chalk it up to same reason as frontend. Maybe someone will sophisticate me in the future? Also I decided to add .dockerignore file at this point to frontend also.

Time for compose file. I found pretty good guide for that that is in the sources and it worked almost instantly after making it. Start it with: Docker compose up. It all started and put the containers nicely in there like this:

![image](https://github.com/aexceed/weatherapp/assets/129611461/263c795c-ccfa-4e71-8361-49e083891211)

Still nothing while clicking the open ports. There was something about not using localhost as the access to site but for the life of me I couldn´t figure it out. This might be a problem with my computer and all the weird settings that I have setup in it over the years. Who knows.

Volumes and hot reload. As far as volumes are concerned I understood that it´s as simple as adding volumes part with service names in to the compose document. I tried searching about hot reload and what to do to achieve it. For me it loads everything up lightning fast. I made reload folder in the weatherapp but I wasn´t quite sure what to do with it. Should I put compose file in there? Does it know where to find front and backend even if they are on same folder tree level as compose file? Couldn´t quite grasp how to do it or if I had allready done it partly with my progress so far so I just left it for now because it´s time to move forward in my assignment.

# Cloud

My public cloud of choice for this part of the assignment is AWS. I have no idea what to expect in getting the containers to work in cloud so time to get started. Apparently AWS has pretty good documentation how to do this so I started following the guide. I created context and set my variables in my git bash inside my weatherapp folder. Changed context to new context with docker context use myecscontext -command. AWS variables I set like this:

![image](https://github.com/aexceed/weatherapp/assets/129611461/ed750243-f0bf-44c7-8edd-24e1c033243e)

Tried to compose up but it gave me warning about unsupported build attribute. Issue turned out to be that I hadn´t uploaded my images to dockerhub. So quick googling how to do that and it was simple command where you tag the image first and then send it to your dockerhub. I also had to login to docker.io throught console for it to work.

![image](https://github.com/aexceed/weatherapp/assets/129611461/bc5f2166-2eb0-456f-afb3-54464cfafbc1)

Did the same for frontend and now they were there. Tried composing it again after changing the attribute to ecs context but it kept giving me the same error about attribute. Thought came to my mind that maybe I have to refer the hub image in my compose file. Went into compose file and changed build to my image: eep97/ * images *. It started working, caught me bit by surprise.

![image](https://github.com/aexceed/weatherapp/assets/129611461/de5768c4-4d31-4a89-95f7-c58f07a6e503)

Went into my AWS console to look and there they actually were, load balancers and everything created.

![image](https://github.com/aexceed/weatherapp/assets/129611461/2b78f8da-a0fb-4c93-ba54-c3925cb0529a)

I just uhh found a slight problem, I could not find the address where to check whatever it is running there the empty nginx page or just about anything. Odd problem to run into but yeah uhh... It obviously launched something but yeah I really dont know what happened. I´ll just put it in the first time using containers in cloud blame basket. I´d be interested to know what really happened and why. Did it shutdown just as fast as it launched and thats why I couldn´t find it? Maybe I should have defined what AWS services it starts and how it configures them in compose document or some other document?

# Ansible

This one is another new one for me so I started by reading how it works and whats the syntax for it. Seems to be as simple as playbook.yml file that does it all. Many sites have information about using it but in linux and well im using windows for now so it might increase the level of difficulty for this. First I need to install ansible. Guide told me I need python first which I did not have in this computer installed so I got that one first from pythons website. Next I went into cmd.exe as admin and used command pip install ansible to install it. Tried checking version for ansible but a weird error about AttributeError: module 'os' has no attribute 'get_blocking'. Something about adding python to system variables so I went ahead and did it but still nothing. Starting to get on my nerves and now I remember again why you should use Linux for this kind of stuff. I might just have to write the file blind and hope it works can´t seem to figure a workaround for this.

# Sources

https://superuser.com/questions/1709437/how-can-i-update-the-kernel-in-wsl2-kernel-to-latest-release Read on 27.9.2023

https://openweathermap.org/current#builtin Read on 28.9.2023

https://siddharth-lakhara.medium.com/dockerizing-a-full-stack-js-app-ceb99411996e Read on 28.9.2023

https://milanwittpohl.com/projects/tutorials/Full-Stack-Web-App/dockerizing-our-front-and-backend Read on 28.9.2023

https://octopus.com/blog/using-nginx-docker-image Read on 28.9.2023

https://hub.docker.com/_/nginx Read on 28.9.2023

https://www.freecodecamp.org/news/how-to-enable-live-reload-on-docker-based-applications/ Read on 28.9.2023

https://medium.com/@kartikio/setup-node-ts-local-development-environment-with-docker-and-hot-reloading-922db9016119 Read on 28.9.2023

https://medium.com/greedygame-engineering/so-you-want-to-dockerize-your-react-app-64fbbb74c217 Read on 28.9.2023

https://shisho.dev/blog/posts/how-to-use-dockerignore/ Read on 28.9.2023

https://docs.docker.com/compose/compose-file/07-volumes/ Read on 30.9.2023

https://docs.docker.com/storage/volumes/ Read on 30.9.2023

https://aws.amazon.com/blogs/containers/deploy-applications-on-amazon-ecs-using-docker-compose/ Read on 1.10.2023

https://www.biostars.org/p/9531985/ Read on 1.10.2023

https://docs.docker.com/cloud/ecs-integration/ Read on 1.10.2023

https://medium.com/@viknesh2798/how-to-fix-the-issues-while-using-python-command-in-the-command-prompt-ba56d9018c5f Read on 2.10.2023

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#control-node-requirements Read on 2.10.2023
