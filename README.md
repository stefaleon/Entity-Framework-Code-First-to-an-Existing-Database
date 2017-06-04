# Entity Framework Code First to an Existing Database
[ Microsoft: Introduction to Entity Framework](https://msdn.microsoft.com/en-us/library/jj200620(v=vs.113).aspx)

&nbsp;
## 00 Start the project
* Create an Existing Database
    * In MSSMS create a database named Blogging.
    * In VS -> View -> Server Explorer -> Data Connections -> Add Connection…
    * Server Name: (localdb)\MSSQLLOCALDB
    * Enter database name: Blogging
    * The new database will now appear in Server Explorer, right-click on it and select New Query
    * Copy the following SQL into the new query, then right-click on the query and select Execute
    ```
    CREATE TABLE [dbo].[Blogs] (
    [BlogId] INT IDENTITY (1, 1) NOT NULL,
    [Name] NVARCHAR (200) NULL,
    [Url]  NVARCHAR (200) NULL,
    CONSTRAINT [PK_dbo.Blogs] PRIMARY KEY CLUSTERED ([BlogId] ASC)
    );

    CREATE TABLE [dbo].[Posts] (
        [PostId] INT IDENTITY (1, 1) NOT NULL,
        [Title] NVARCHAR (200) NULL,
        [Content] NTEXT NULL,
        [BlogId] INT NOT NULL,
        CONSTRAINT [PK_dbo.Posts] PRIMARY KEY CLUSTERED ([PostId] ASC),
        CONSTRAINT [FK_dbo.Posts_dbo.Blogs_BlogId] FOREIGN KEY ([BlogId]) REFERENCES [dbo].[Blogs] ([BlogId]) ON DELETE CASCADE
    );

    INSERT INTO [dbo].[Blogs] ([Name],[Url])
    VALUES ('The Visual Studio Blog', 'http://blogs.msdn.com/visualstudio/')

    INSERT INTO [dbo].[Blogs] ([Name],[Url])
    VALUES ('.NET Framework Blog', 'http://blogs.msdn.com/dotnet/')

    ```
* Create a Console Application. Enter CodeFirstExistingDatabaseSample as the name.  
