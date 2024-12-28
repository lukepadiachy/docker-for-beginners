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

### Adding Nuget Packages Needed

![image](https://github.com/user-attachments/assets/f3deab8e-8584-4a53-a4ad-c73418c63005)

To do this for your own project:
- Right-Click on your api project (eg: mine is bookstore.Api )
- Head to **`manage nuget packages`**
- Make sure you are in the `Browse` tab
- Search `Microsoft.EntityFrameworkCore`
- Then install and accept
- That's just 1 , you got 3 more to do, you can simply add a dot at the end of `Microsoft.EntityFrameworkCore` and say `Microsoft.EntityFrameworkCore.Design`, `Microsoft.EntityFrameworkCore.Tools` & `Microsoft.EntityFrameworkCore.SqlServer`

![image](https://github.com/user-attachments/assets/7a70d309-2376-4ecf-aac1-57fe5d5eb870)


So if you do not have `.NET 9`, do not copy the packages Im providing below because these are for that.

```markdown
<PackageReference Include="Microsoft.AspNetCore.OpenApi" Version="9.0.0" />
<PackageReference Include="Microsoft.EntityFrameworkCore" Version="9.0.0" />
<PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="9.0.0">
  <PrivateAssets>all</PrivateAssets>
  <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
</PackageReference>
<PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="9.0.0" />
<PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="9.0.0">
  <PrivateAssets>all</PrivateAssets>
  <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
</PackageReference>
<PackageReference Include="Swashbuckle.AspNetCore" Version="7.2.0" />
```

You can double-click on your api project to make sure all packages are there , rebuild/run your project to make sure everything is good.

![image](https://github.com/user-attachments/assets/2427a8bf-7134-4a16-9644-7877bb56afae)

### Adding Models
Now that we have our packages needed , **LET'S COOK**. We will be making sure that we add the information needed to set up our EF Core proceess, some might know this process already.

- Created a folder called **`Model`**
- Moved **`WeatherForecast.cs`** into that folder (OCD purposes)
- Created a class called **`Book.cs`**
- Added properties
- This will define our table for the database

```markdown
public class Book
{
    public int BookId { get; set; }
    public string Title { get; set; }
    public string Author { get; set; }
    public string Genre { get; set; }
    public decimal Price { get; set; }
    public int Pages { get; set; }
    public string Publisher { get; set; }
}
```
### Adding Configurations
So we got our model, lets take this piece of the puzzle and connect it.

- Created a folder called **`Data`**
- Adding a class in that folder called **`BookStoreDbContext.cs`**

   ```markdown
  public class BookStoreDbContext : DbContext
  {
    public BookStoreDbContext(DbContextOptions<BookStoreDbContext> options) : base(options)
    {
    }

    public DbSet<Book> Books { get; set; }
  }
  ```
- Adding another class in the **`Data`** Folder called **`BookConfiguration.cs`**
- Won't provide the code block because it is quite big , but this file is what we will use to seed our Database
- Head back to our **`BookStoreDbContext.cs`** class and add the code block below inside it
  ```markdown
  protected override void OnModelCreating(ModelBuilder modelBuilder)
  {
    base.OnModelCreating(modelBuilder);
    modelBuilder.ApplyConfiguration(new BookConfiguration());
  }
  ```
- something I picked up afterwards , if you do not add this , It will not seed your database with information.

![image](https://github.com/user-attachments/assets/218265ea-f959-486d-89db-4058d250d27f)

- Head over to the **`Program.cs`**
- Let's add our DbService basically
  
  ```markdown
  builder.Services.AddDbContext<BookStoreDbContext>(options => {
    options.UseSqlServer(builder.Configuration.GetConnectionString
        ("BookStoreDatabaseConnection"));
  });
  ```

- Keep in mind at this point we dont have our connection string yet , so we going to add it in our **`appsettings.json`**

  ```markdown
  "ConnectionStrings": {
  "BookStoreDatabaseConnection": "Server=localhost, 1400;Database=MusicStoreDb;Trusted_Connection=false;MultipleActiveResultSets=true;Encrypt=false;user id=sa;password=Str0ngPa$$word;"
  },
  ```
  
- This will be pointing at our Database in **Docker** , if you don't know how to do this, refer to [Containerizing Your SQL Server Database With Docker](https://github.com/lukepadiachy/docker-for-beginners/blob/main/docker-essentials/1.Containerizing%20Your%20SQL%20Server%20Database%20With%20Docker.md)
- So since we using of dockerised SQL Server from the get-go , be mindful of your port you used in the set up of your SQL Server on Docker , in my setup I used `1400` , so it would be `1400:1433`


