### Introduction

While our default templates designed to work with SQL Server, you can
easily modify them to work with MySql. In order to do that, you need to
follow below steps.

#### Download Project

Go to <http://aspnetboilerplate.com/Templates> and download a new
project. Select ASP.NET MVC 5.x tab and don't forget to select Entity
Framework.

#### Install MySql.Data.Entity

Then you need to install
[MySql.Data.Entity](https://www.nuget.org/packages/MySql.Data.Entity/)
nuget package to your **.EntityFramework** and **.Web** projects.
Installing this nuget package to your **.Web** project should make
necessary changes in your web.config file.

Open your DbContext's configuration class (Configuration.cs) and place
below code in it's constructor

    SetSqlGenerator("MySql.Data.MySqlClient", new MySql.Data.Entity.MySqlMigrationSqlGenerator());

#### Configure ConnectionString

You need to change your connection string in the web.config file in
order to work with your MySql database. An example connection string
would be

    <add name="Default" connectionString="server=localhost;port=3306;database=sampledb;uid=root;password=***" providerName="MySql.Data.MySqlClient"/>

#### Re-generate migrations

If you choose "Include module zero?" while downloading your startup
template, there will be some migration files included in your project
but those files are generated for Sql Server. Delete all migration files
in your **.EntityFramework** project under Migrations folder. Migration
files start with a timestamp. A migration file name would be like this
"201506210746108\_AbpZero\_Initial"

After deleting all migration files, select your **.Web** project as
startup project, open Visual Studio's Package Manager Console and select
**.EntityFramework** project as default project in Package Manager
Console. Then run below command to add migration for MySql.

    Add-Migration "AbpZero_Initial"

Now you can create your database using below command

    Update-Database

It is all done, now you can run your project with MySql.