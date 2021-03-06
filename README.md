# Validation Microflow Creator
## Installation
Set up your development tools by following the steps in this article:

[https://docs.mendix.com/apidocs-mxsdk/mxsdk/setting-up-your-development-environment](https://docs.mendix.com/apidocs-mxsdk/mxsdk/setting-up-your-development-environment)

Clone the repository to a folder on your local pc and then open the folder in a command prompt. 

Install project dependencies by running the following command

`npm install`

## Configuration

In the src folder, update the file config.json.

### auth

```
{
    "auth" : {
        "username":"",
        "apikey":""
    }
    ...
}
```

**auth.username**: Your Mendix login (i.e. your email address)

**auth.apikey**: An api key that you have generated for your Mendix login (not a project api key)

### project
```
{
    ...
    "project":{
        "id":"",
        "name":"",
        "branch": ""
    }
    ...
}
```

**project.id**: The id of your project

**project.name**: The name of your project

**project.branch**: The name of the branch you want to use (or empty string for the main line)

### app
```
{
    ...
    "app":{
        "folderName" : "_sdk-autogenerated",
        "validationMicroflowPrefix" : "SUB_Validate",
        "validVariableName" : "IsValid",
        "requiredFieldMessage" : "This field is required.",
        "modules":[{
            "name":"",
            "entities":[""]
        }]
    }
}
```

**app.folderName**: The name of the folder to store all generated microflows (will create the folder if it does't exist)

**app.validationMicroflowPrefix**: The prefix for the microflow names that will be created (the entity name will be appended to the end)

**app.validVariableName**: The name of the boolean variable that will be created to hold the validation state of an object in the microflow

**app.requiredFieldMessage**: The string to be used in the validation feedback activity if an attribute fails its validation check (currently there is no support for multiple languages so this string will be used for all languages in the project)

**app.modules**: An array of modules that you wish to create validation microflows for.

**app.modules[n].name**: The name of the module (Required)

**app.modules[n].entities**: A list of strings containing the entity names you want to create validation microflows for. Pass an empty array to process all entities.

## Exclusive split expressions
The supported data types and the expression template used to determine whether an attribute of that type is valid or not is held in a constant called typeSplitExpressions declared towards the top of script.ts

The data types can be extended as required. Possible types are listed on the following page:

[https://apidocs.mendix.com/modelsdk/latest/modules/domainmodels.html](https://apidocs.mendix.com/modelsdk/latest/modules/domainmodels.html)

The expression template function can also be changed if required. The value `${variableName}` will be replaced with the attribute name at run time.  

## Run the script
Compile the script by running the following command:

`tsc`

Run the script with the following command:

`npm start`

Once the script has completed you can update your project in the modeller to see the new microflows.