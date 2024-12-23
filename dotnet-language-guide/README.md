# :heart_decoration: .NET language-specific guide
After completing all the tutorials on docker desktop, you will have a couple of language specific guides which you can go for. I went for the `.NET` guide, since this is what I work with on a daily. 
The time specified on the docs is 20 minutes, It took me about a day to get a grasp of it, choice of words.. grasp. While working with this guide, I made sure to read through the information properly, there was some bumps here and there which I will specify how I overcame them. 

![image](https://github.com/user-attachments/assets/1c314761-69aa-4cb3-9414-5b759b5176e4)

![image](https://github.com/user-attachments/assets/b490a864-7467-4213-9385-e83d7577c00a)


# 🔍 Specifics

- [Containerize and run a dotnet application](#containerize-and-run-a-dotnet-application)
- [Set up a local environment to develop a dotnet application using containers](#set-up-a-local-environment-to-develop-a-dotnet-application-using-containers)
- [Run tests for a dotnet application using containers](#run-tests-for-a-dotnet-application-using-containers)
- [Configure a CI/CD pipeline for a containerized dotnet application using GitHub Actions](#configure-a-ci-cd-pipeline-for-a-containerized-dotnet-application-using-github-actions)
- [Deploy your containerized application locally to Kubernetes to test and debug your deployment](#deploy-your-containerized-application-locally-to-kubernetes-to-test-and-debug-your-deployment)


## Containerize and run a dotnet application
This was something I followed when creating my own web app with docker in order to create a sample app for beginners to go through (I say this as if im not one , I am a beginner still). You can follow the steps in this as is.
If you would like to go for gold , you can look at this [**blogpost**](https://www.docker.com/blog/building-multi-container-net-app-using-docker-desktop/) which gives you the breakdown of how the  pre-built application in the tutorial was made.

![image](https://github.com/user-attachments/assets/ccfa85c1-f227-45f4-8598-d173b5ee8c98)

## Set up a local environment to develop a dotnet application using containers
I remember having some small issues with this section, they were more related to small typos. Something to note , you will be looking at a different branch in this module. Since you already cloned the repo, I assume you still got the IDE open. 
You can follow the commands provided ` git stash -u` & then `git checkout add-db`, what you doing here is going to the branch which has the database within it. You will be uncommenting code in here too , don't forget to highlight the section and use shortcut `ctrl + k`, 
then `ctrl + u`. Then `ctrl + s` to make sure its saved :). If you are following this guide. note to click on the local host link provided within the guide, since the port specified is that one.

![image](https://github.com/user-attachments/assets/1284bbb7-80eb-4cee-b30e-bd64231cf9f3)

You will be adding a db folder within the project and creating a file called password.txt, it would like this below:

![image](https://github.com/user-attachments/assets/ea3b76b8-5273-490b-b147-dd9434f2b0e1)

This will go underneath DOCKER-DOTNET-SAMPLE

| Adding a folder         | Adding a file        |
|-----------------------------|-----------------------------|
| ![image](https://github.com/user-attachments/assets/f334482e-83ac-49a0-ac6c-4cd05ae1b69a)| ![image](https://github.com/user-attachments/assets/f68aebc2-31fa-427c-9d8b-ed8e7aca156f)|

Ahh I remember now , my issue was due to not saving haha, your db wont be pulled if the information is not correct for the files you added for the db

![image](https://github.com/user-attachments/assets/166966c7-b967-434d-8fc1-e30af58f9048)

You will be adding your information to the database manually through the terminal., if you want , you can `ctrl + c` inside the terminal to stop the run. If not and you want to continue with the adding of information to the db , you will have to open another terminal.
The shortcut for another terminal will be ``ctrl + shift + ` ``. something to note when you do the command for `docker exec -it 39fdcf0aff7b psql -d example -U postgres`, for replacing the id , i copied it to my notepad , then replaced id number with my own after this, then dropped it into my terminal like below.

![image](https://github.com/user-attachments/assets/8b79ca14-986c-490d-be5e-faeb157593f9)

Once you got that set up you can do the same with `INSERT INTO "Students" ("ID", "LastName", "FirstMidName", "EnrollmentDate") VALUES (DEFAULT, 'Padi', 'Luke', '2024-12-23');` , I changed this within my notepage, for some reason , I could not `ctrl + v` into the example thing. 
So I clicked in that space then right-clicked on my mouse and it dropped the info of Insert (lol DROP & INSERT, wooow). I need to up my english. Using pasted in a sentence didnt seem like a cool thing , so im replacing it with "dropping". Back on topic , no need to copy the example= part with it , just from Insert onwards.

![image](https://github.com/user-attachments/assets/3c73325c-31cd-4861-8cd8-52c713e30029)

If everything went well it should look like this with your name:

![image](https://github.com/user-attachments/assets/08a8f802-1403-473c-89c6-1aa6065b0563)

If you created a new terminal , dont forget to close it. If you are using an exisiting one , you can continue with the rest of the instructions.

Let's talk weird errors you might see, reason for this was me being funny , I did not save the information I added to my `compose.yaml` file so it crassshed.

![image](https://github.com/user-attachments/assets/11249dd2-e865-4ecc-a192-1ee04669b3e1)

Saving is important!

You will be introduced to [**Multi-stage builds**](https://docs.docker.com/build/building/multi-stage/), I think we could use a game analogy for this? Like you know you get multi-player and single player right? It's kinda like that , you have 1 game with two differnt ways to play , Single player has 1 screen and Multi , well 2 or even 4 screens.
So if we looking at it from a dev's view , you can use multi-stage builds to build stages for both development and production in the same Dockerfile(same game). 

## Run tests for a dotnet application using containers
This one was pretty straight forward, struggles did not really find me with the testing part. Probably because this was somewhat plug and play in terms of the commands we used and code we dropped in the files.

![image](https://github.com/user-attachments/assets/e331a7ce-d248-44a8-baaf-fe2038050dd1)

## Configure a CI/CD pipeline for a containerized dotnet application using GitHub Actions
This section showed me flames at 1 am in the morning, you will be introduced to GitHub Actions, this was my first time doing that and I can say wow , really interesting what happens there, it's giving Azure DevOps vibes. This might be abit detailed , due to some struggles I faced while following /not follwing instructions.
Im not sure if it was due to the time or me trying to freestyle this part. LETS DO THIS !!!

At this point I assume you:
- Completed all the previous modules before this
- Have a GitHub Account and a Docker Account
- No GitHub ? No problemo, sign up [**today**](https://github.com/login)

### Creating the repository
1. Create the repo on GitHub
   
   ![image](https://github.com/user-attachments/assets/ef50ea45-7af4-4fcf-8467-1b6f1d2b03f4)

2.Open the repository Settings, and go to Secrets and variables > Actions.

  ![image](https://github.com/user-attachments/assets/450946ab-86f6-40ff-be65-87307451979f)

3.Create a new Repository variable named `DOCKER_USERNAME` and your Docker ID as value.

  **BE WARY OF TYPOS**
  Inside here you will click the Variable tab , then Click `New Repository Variable` and add required information, when they mention Docker ID, they legit mean your username for Docker when you signed up.
  ![image](https://github.com/user-attachments/assets/9104e0cb-f9cf-4db4-a56e-2bad68f0587a)

4.Create a new Personal Access Token (PAT) for Docker Hub. You can name this token `docker-tutorial`. Make sure access permissions include Read and Write.

  This section was abit overwhelming when I did it the first time , I think I did this twice because hebana..
  There was light at the end of the tunnel though, be sure to follow this [Personal Access Token (PAT)](https://docs.docker.com/security/for-developers/access-tokens/#create-an-access-token), in this process you might see a token already there, you can ignore that and create a new one.
  So when you creating your token don't forget description , in the docs you were asked to name your token `docker-tutorial` with permissions like Read & Write.
  It will look something like this:
  
  ![image](https://github.com/user-attachments/assets/ef7a489f-89db-4708-b8d3-5ba600e2eba8)

  Once you click generate , you will see two options to copy its the second one with the weird numebrs and letters , be sure to either copy it to your clipboard or drop it inside your notepad

5.Add the PAT as a Repository secret in your GitHub repository, with the name `DOCKERHUB_TOKEN`.
  
  **BE WARY OF TYPOS**
  Inside here you will click the Secrets tab , then Click `New Repository Secret` and add required information, when they mention Secret , this will be the token you generated for yourself.

  ![image](https://github.com/user-attachments/assets/6f4d777a-818c-4143-ae24-f41f4cfa7767)

6.In your local repository on your machine, run the following command to change the origin to the repository you just created. Make sure you change `your-username` to your GitHub username and `your-repository` to the name of the repository you created.
  
  I won't lie , this part had me stuck for a minute. Maybe I read this wrong , but for some reason I did not know that this meant:
  
  - Head over to the repo you were working on `docker-dotnet-sample`, on your machine itself.
  - Once inside the directory open your command line , you can basically just type `CMD` in the Directory bar which shows your file path , this is next to the search bar , make sure that you are inside of the docker-dotnet-sample folder
  - Then use their commands `git remote set-url origin https://github.com/your-username/your-repository.git` within the command line
  - Remember to replace `your-username` and `your-repository.git` with the actual details from the new repository you created
  - If you still got your tab open where you did all the GitHub stuff you can actually Click on the `code` tab, this should still be an empty repo basically , then copy the link provided underneath `Quick Setup` then you can go to your notepad and customise you command and just replace the one you had with the one you got from GitHub. 
  
  So your command line should look something like this:

  ![image](https://github.com/user-attachments/assets/0bf80444-0ca9-47cb-b58f-9001b8ecea51)

  If you refresh your repo, you should now see files inside like this:

  ![image](https://github.com/user-attachments/assets/0ddbdb01-1ebb-4575-81d2-3243c74975d6)


  Yeah that was abit confusing for me at the start, I could also be doing this wrong, but it worked so I moved along.

  ### Setting up the workflow

  Did not have much issues here , It failed before due a typo in one of my secrets or repository variable.
  So if you on the happy path , it should display like such:

  ![image](https://github.com/user-attachments/assets/c8035f94-5961-4303-b1dd-94dd4beccadb)

  ## Deploy your containerized application locally to Kubernetes to test and debug your deployment
  This was my first time being introduced to Kurbernetes. Kubernetes is like a group Project Lead for Docker containers. 
  It makes sure each container (team member) knows what to do, gets enough resources, and keeps working even if one messes up. It’s like a teacher organizing a class project—assigning tasks, keeping backups, and making sure everything runs on time.

  This was also abit straight forward 

  Don't forget to turn on Kurbernetes first inside of you Docker Desktop for this module, not too sure how important this section was in terms of learning docker, but it was really interesting to do and im sure it's there for a reason, something I will be looking more into. 

  ![image](https://github.com/user-attachments/assets/cac7b190-ae61-422e-acc9-ed41db0c3190)

  If by anychance you confused by this part of the module `Replace DOCKER_USERNAME/REPO_NAME with your Docker username and the name of the repository that you created in Configure CI/CD for your .NET application.`

  You can find this in your Images section in the Docker Desktop:

  ![image](https://github.com/user-attachments/assets/c2e0e7e5-b924-4178-a47a-2f0a0177162b)

  Once you've done this , you basically free to explore any more avenues of docker :) , CONGRATS !!!
  

