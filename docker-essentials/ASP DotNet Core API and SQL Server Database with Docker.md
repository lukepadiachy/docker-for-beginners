# 🌐 ASP.NET Core API & SQL Server Database With Docker

![Containerizing  Your ASP NET Core API  With Docker (2)](https://github.com/user-attachments/assets/3a7d7de0-d2c1-4bcd-ad7c-0088c14f4f62)

This was an interesting one that took me about two days to figure out how it actually works after watching some videos on it. This definetly involves getting your hands dirty with some code. Please note that we are using `.NET 9`.
The idea with this doc is more for those interested in connecting their SQL Server which has been Dockerised with a ASP.NET Core Web API. I will be going through some of the code. This is more focused on connecting two pieces of a puzzle.
Once we have connected those pieces of the puzzle. We will see that a Docker file can basically be added at any point of your development process, I hope.

# 🔍 Specifics

- [Create Your ASP DotNet Core Web API](#create-your-asp-dotnet-core-web-api)
- [Connect ASP DotNet Core Web API to a Dockerised SQL Server Database](#connect-asp-dotnet-core-web-api-to-a-dockerised-sql-server-database)




## Create Your ASP DotNet Core Web API
Keep in mind I'm using `.NET 9` , with that being said , you can either `clone` this repo (assuming you have Git) [book-store](https://github.com/lukepadiachy/book-store) or create it yourself. I have made a small video so you can see how to create it in `Visual Studio`.
[Video Link](https://drive.google.com/file/d/1_yarqwPwK4E_cqg86MDsKcZU9I514VET/view?usp=sharing). If you are using my repo , note I have added swagger to it, as this does not come with ASP.NET Core Web API for `.NET9` , older versions should still have it. So if you decided to create your own repo for this on `.NET9`.
Here's a link to show you how to incorporate it in your project : [.NET9 Swagger Integration](https://github.com/Menayer/DotNet9-Swagger-Integration).

![image](https://github.com/user-attachments/assets/21ef65b0-a020-45cc-8a66-ccea3df6231e)

## Connect ASP DotNet Core Web API to a Dockerised SQL Server Database
