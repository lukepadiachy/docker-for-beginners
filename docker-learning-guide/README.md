# 🎓Docker's Learning Guide For Beginners
Honestly enjoyed this process, usually tutorials/walkthroughs can take a lot of your time when they're new to you. Started out with this learning guide right after the installing Docker. Short , sweet and simple is the best way to describe how they packaged this.
You will find more documentation as you start getting to specific parts of the walkthroughs which will be good to read on.


![image](https://github.com/user-attachments/assets/99e1e58b-040d-4b3b-97b8-cb28cbf74694)

# 🔍 Specifics

- [What is a container?](#what-is-a-container)
- [How do I run a container?](#how-do-i-run-a-container)
- [Run Docker Hub images](#run-docker-hub-images)
- [Multi-container applications](#multi-container-applications)
- [Persist your data between containers](#persist-your-data-between-containers)
- [Access your local folder from a container](#access-your-local-folder-from-a-container)
- [Containerize your application](#containerize-your-application)
- [Publish your image](#publish-your-image)


## What is a container?
So the cool thing about this section is that they actually create a welcome container for you? I mean like huuh? I already created my first container just by clicking on a guide? sorcery. 

![image](https://github.com/user-attachments/assets/93088fc1-1796-45d8-8339-d8767ea3d6a7)

This section was pretty straight forward , there wasn't much weird things happening when I tried this out.

## How do I run a container?
Learn how to run your own one now. You will have to clone a repo.
What if you dont know how to clone a repo?

Here's some docs:
[Cloning a repo](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) 

You will also find yourself in the IDE of your choosing, checking out some code. I mentioned before, due to the tutorial giving off a Visual Studio Code vibes only, I went that route.

**SOME CHEATCODES**
| Step 1 | Step 2 |
|--------|--------|
| ![Step 1](https://github.com/user-attachments/assets/fd09d410-2724-4879-b009-5e0537dced0a) <br> Once inside your welcome-to-docker folder type `cmd` in the top bar | ![Step 2](https://github.com/user-attachments/assets/c65b214b-7a0c-4c4b-960e-03a0af2a8acc) <br> After hitting Enter, you will have the command line open then type in `code .` which will open the IDE |

Have a browse through the files that the tutorial will be taking you through, especially the breakdown of commands for the terminal

## Run Docker Hub images
In this section you will start seeing some things that will make more sense as you go about.

![image](https://github.com/user-attachments/assets/53225ea8-10f5-4034-b0a0-7c3ae3cfbcc7)

## Multi-container applications
This is where things start getting spicy, it goes from just being one container to many containers with only one command, Introducing a tool known as **Docker Compose**. I feel like whenever something gets compose added next to it , immediately it becomes "oh look at me , I can do so much more" 

Also make sure that if you dont copy and paste commands for whatever reason and type them out manually, be sure that these commands are TO THE T, sometimes I felt abit like "ahh let me rather type this and boom error , only to see its a typo".

![image](https://github.com/user-attachments/assets/5b34da42-19d3-46de-a528-bd4020bd5490)

There will be some docs for [compose watch documnentation](https://docs.docker.com/compose/how-tos/file-watch/)

![image](https://github.com/user-attachments/assets/7fac31be-7452-40fe-a57e-63e265057dca)

Don't be afraid to delete it.. there's a reason for everything.

## Persist your data between containers
In otherwords , how can I make the information that's inside my database stubborn? Kinda like Insurance Agents, just because you cancelled your policy with one , does not mean another wont call having your exact info(super werid). You will be introduced to **volumes**. Some hot-keys for the Windows users, you will be uncommenting some code. Highlight the code that has been commented out then `ctrl + k` & then `ctrl + u`, this will uncomment the highlighted section. Remember to have a look at the text that are under the code boxes too in the guides, these are gold.

**Things to note:**
- Once code is uncommented , run the project again in terminal
- Make sure that volume is mentioned within terminal output after command
- To test if data persists , add some tasks first
- Delete the multi container
- Then build again and see your stubborn data
- Dont forget to save files in IDE (Trust me)

![image](https://github.com/user-attachments/assets/15a8f295-0ec6-431e-8c40-4cdf88851098)

## Access your local folder from a container
Bind Mounts ? WHAT ARE THOOOSE ?? It's like a direct link between your computer and a container. It lets the container access files or folders from your computer in real-time.












