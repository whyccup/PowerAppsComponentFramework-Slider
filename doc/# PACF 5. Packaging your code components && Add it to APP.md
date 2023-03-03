# PACF 5. Packaging your code components && Add it to APP

Follow these steps to create and import a solution file:

1. Create a new folder named Solutions inside the LinearInputControl folder and navigate into the folder.

```CLI
mkdir Solutions
  cd Solutions
```

2. Create a new solution project in the LinearInputControl folder using the pac solution init command

```CLI
pac solution init --publisher-name Samples --publisher-prefix samples
```

***
The publisher-name and publisher-prefix values must be the same as either an existing solution publisher, or a new one that you want to create in your target environment.
You can retrieve a list of current values using this query on your target environment:
[Environment URI]/api/data/v9.2/publishers?$select=uniquename,customizationprefix
More information: Query data using the Web API
***

3. Once the new solution project is created, you need to refer to the location where the created component is located. You can add the reference by using the following command:

```CLI
pac solution add-reference --path ..\..\
```

4. To generate a zip file from your solution project, when inside the the cdsproj solution project directory, using the following command:

```CLI
msbuild /t:restore
```

Or if you have installed the .NET 6 SDK:

```CLI
dotnet build
```

5. Run the following command again:

```CLI
msbuild
```

***
If you receive the error Missing required tool: MSBuild.exe/dotnet.exe. Add MSBuild.exe/dotnet.exe in Path environment variable or use Developer Command Prompt for Visual Studio Code. As mentioned in Prerequisites, you must install .NET build tools.
***

***
You will see the message Do not use the eval function or its functional equivalents, when you build the solution file using the msbuild command and import it into Dataverse and run the solution checker. Re build the solution file using the command msbuild/property:configuration=Release and reimport the solution into Dataverse and run the solution checker. More information: Debug code components.
***

6. The generated solution zip file is located in the Solution\bin\debug folder.
7. Manually import the solution into Dataverse using PowerApps once the zip file is ready or automatically using the Microsoft Power Platform Build Tools.

## Add your code component to an app

To add a code component to an app, follow the steps in these articles:

1. Add components to columns and tables for model-driven apps
2. Add code components to a canvas app
3. Use code components in portals
