# Exercise - Write code to implement a web application

* 10 minutes

In this unit, you will use developer tools to create the C Sharp code for a starter web application.

## Login to the Azure Portal

1. Open the [Azure portal](https://portal.azure.com) in a browser.

2. Sign into Azure using the Microsoft account email address and password you created for this session.

## Create a new web project

The heart of the .NET CLI tools is the `dotnet` command line tool. Using this command, you will create a new ASP.NET Core web project.

1. In the Cloud Shell, create a new ASP.NET Core MVC application. Name it _TestWebAppXXXXXXX_, where _XXXXXXX_ is a word or number you add to give the web app a unique name.

    dotnet new mvc --name TestWebAppXXXXXXX

2. The command will create a new folder named _TestWebAppXXXXXXX_ to hold your project. `cd` there, then build and run the application to verify it is complete.

    cd TestWebAppXXXXXXX

    dotnet run

    You should get something like:

        Hosting environment: Development
        Content root path: /home/your-user/TestWebAppXXXXXXX
        Now listening on: https://localhost:5001
        Now listening on: http://localhost:5000
        Application started.

    The output describes the situation after starting your app: the application is running and listening at port 5000.

    If we were running the app on our own machine, we'd be able to open a browser to http://localhost:5000 and see our site. To make this accessible from outside of our own machine, we'll need to deploy the app to somewhere with a public endpoint. The App Service instance we created earlier is perfect for that.

3. Press _Ctrl+C_ to shut down the running app.

Congratulations! You just created the code for a Web App, in the Azure Cloud Shell.
