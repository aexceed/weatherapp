# My documentation

My computer specifications that im doing the assignment with:

OS: Windows 10 Home

Processor: Intel(R) Core(TM) i7-4770K CPU @ 3.50GHz

GPU: GeForce GTX 1080

RAM: 16 gt

Ancient "gaming" PC that can shut off and freeze at any moment and works in mysterious ways.

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

Trying to get the whole thing working instantly instead of putting smaller parts together I started frontend Dockerfile first. For the frontend Dockerfile, I need some engine to host my website and I chose nginx. Installed extension to my docker and made Dockerfile based on ideas from internet. Had some trouble getting it to work but then I added script to package.json file and it started doing something. For some reason my page only showed the basic nginx page instead of that file I was given. Tried to get it to work but it was hopeless. Thought came to my mind that maybe I needed to do react part of the tasks to have it really working so I just left it like that. I got my container to start and show something that´s gotta count for something right? You can read more of my thoughts (if there was any sense in them) about that one inside the Dockerfile comments. 

Now for the backend I chose same alpine but yarn instead of npm for package manager, this one was pretty simple compared to frontend in my mind. Some googled parts of code and it ran pretty much straight away. I also found out about .dockerignore file to hide some of the files that are unneccessary and take less space for Docker image so I added it and couple lines in there that seemed to be best practices. Starting the container and checking if the port shows anything and nothing showed up. I´ll chalk it up to same reason as frontend. Maybe someone will sophisticate me in the future? Also I decided to add .dockerignore file at this point to frontend also.

Time for compose file. I found pretty good guide for that that is in the sources and it worked almost instantly after making it. Start it with: Docker compose up. It all started and put the containers nicely in there like this:

![image](https://github.com/aexceed/weatherapp/assets/129611461/263c795c-ccfa-4e71-8361-49e083891211)

Still nothing while clicking the open ports. There was something about not using localhost as the access to site but for the life of me I couldn´t figure it out. This might be a problem with my computer and all the weird settings that I have setup in it over the years. Who knows.

# Cloud

# Ansible

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

