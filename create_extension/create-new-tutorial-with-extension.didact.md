# Creating a new Didact tutorial and registering it with the Didact Tutorials view!

Didact is an extension for VS Code that provides a way to create interactive tutorials using either Markdown or AsciiDoc.  The tutorial user clicks on:

* Prerequisites - In the background VS Code runs the necessary commands to check software installations.
* Commands - VS Code runs the associated command(s) in a terminal that's controlled by the tutorial.

**Additional information**
See the [VSCode Didact readme](https://github.com/redhat-developer/vscode-didact/blob/master/README.md) for more information about other Didact features.

This Didact-based tutorial will walk you through the steps required to create a new VS Code extension that registers a new Didact tutorial.

## Steps

* Use Yeoman and the VS Code Extension Generator to create a TypeScript-based extension project
* Create a Didact Markdown file (and test that it renders correctly in the Didact window)
* Add code to extension.ts to register the Didact file
* Run your extension in a new Extension Development Host window and verify that the new tutorial was registered and available in the `Didact Tutorials` view.

## Prerequisites 

You must have a few things set up prior to walking through the steps in this tutorial. 

<a href='didact://?commandId=vscode.didact.validateAllRequirements' title='Validate all requirements!'><button>Validate all Requirements at Once!</button></a>

| Requirement (Click to Verify)  | Availability | Additional Information/Solution |
| :--- | :--- | :--- |
| [Yeoman is already installed](didact://?commandId=vscode.didact.requirementCheck&text=yo-requirements-status$$yo%20--version$$3&completion=Yeoman%203.0.0+%20is%20available%20on%20this%20system. "Tests to see if `yo --version` returns version 3"){.didact} 	| *Status: unknown*{#yo-requirements-status} | If not, check out [Getting Started With Yeoman](https://yeoman.io/learning/) and install Yeoman using npm (`npm install -g yo`) ([click here to install Yeoman using an embedded VS Code terminal window](didact://?commandId=vscode.didact.sendNamedTerminalAString&text=installyeoman$$sudo%20npm%20install%20-g%20yeoman&completion=installed%20yeoman "Install Yeoman in the system"))
| [The VS Code Extension Generator is already installed](didact://?commandId=vscode.didact.requirementCheck&text=generator-requirements-status$$npm%20ls%20-g%20--depth=0%20generator-code$$generator-code@&completion=generator-code%20Yeoman%20generator%20is%20available%20on%20this%20system. "Tests to see if the generator-code Yeoman generator is available"){.didact} 	| *Status: unknown*{#generator-requirements-status} | If not, use `npm install -g generator-code` or `sudo npm install -g generator-code` ([click here to install the generator using an embedded VS Code terminal window](didact://?commandId=vscode.didact.sendNamedTerminalAString&text=installgenerator$$sudo%20npm%20install%20-g%20generator-code&completion=installed%20generator-code%20yeoman%20generator "Install the Yeoman generator-code generator in the system"))
| [At least one folder exists in the workspace](didact://?commandId=vscode.didact.workspaceFolderExistsCheck&text=workspace-folder-status&completion=A%20valid%20folder%20exists%20in%20the%20workspace. "Ensure that at least one folder exists in the user workspace"){.didact} | *Status: unknown*{#workspace-folder-status} | If not, create a workspace folder (or [click here to create a temporary folder](didact://?commandId=vscode.didact.createWorkspaceFolder&completion=Created%20temporary%20folder%20in%20the%20workspace. "Create a temporary folder and add it to the workspace."){.didact}), close, and reopen the Didact window

## Creating a new VS Code Extension

The Visual Studio Code site has a great tutorial on creating a new VS Code extension [here](https://code.visualstudio.com/api/get-started/your-first-extension). We are going to leverage that approach for our new extension.

1. [Call `yo code`](didact://?commandId=vscode.didact.sendNamedTerminalAString&text=runyocode$$yo%20code&completion=started%20generator-code%20generator "Start the VS Code Extension Generator")
2. Specify `New Extension (TypeScript)`
3. Provide the name for your new extension (perhaps `first-didact-tutorial`)
4. Use the defaults and specify `npm` as the package manager

## Creating a New Didact Tutorial File

Didact can consume either a Markdown (`*.didact.md`) or AsciiDoc (`*.didact.adoc`) formatted file. Use either of the following links to create a template file for your tutorial. If no folder is selected in the Explorer, the file will be placed in the first root folder found. Otherwise, it will be placed in the selected folder.

* [Create a new Didact tutorial using the Markdown format](didact://?commandId=vscode.didact.scaffoldProject&extFilePath=redhat.vscode-didact/create_extension/md-tutorial.project.didact.json&completion=Created%20starting%20Didact%20file.)
* [Create a new Didact tutorial using the AsciiDoc format](didact://?commandId=vscode.didact.scaffoldProject&extFilePath=redhat.vscode-didact/create_extension/adoc-tutorial.project.didact.json&completion=Created%20starting%20Didact%20file.)

### Testing the Tutorial File in the Didact window

Select your new tutorial file in the Explorer view and select `Didact: Start Didact Tutorial from File` or [click here](didact://?commandId=vscode.didact.startDidact).

## Registering the New Tutorial

Open the `extension.ts` file and do the following:

* Use the Didact snippet (`Ctrl+Space`) in the editor to add the `registerTutorialWithDidact` method. 
* Change the values for `tutorialName`, `tutorialPath`, and `tutorialCategory` to suit your needs. Remember that if you register multiple tutorials and want them all to be under the same category, you must use the same category name for each.
* Add `registerTutorialWithDidact(context);` to the `activate` function
* In your `package.json` file, change `activationEvents` from `onCommand:extension.helloWorld` to `*`.
* Make sure everything is saved and start a new workspace with your `first-didact-tutorial` folder as the root.

## Running the Extension and Testing your Didact file

VS Code offers the ability to debug your extension, launching another window and connecting the debugger for breakpoint support. To set this up, you will need to [create a Launch Configuration](https://code.visualstudio.com/docs/editor/debugging#_launch-configurations). 

Then, inside the editor, press `F5`. This will compile and run the extension in a new Extension Development Host window.

In the `Didact Tutorials` view, once your extension has finished activating, look for the category you registered your tutorial with in the last step and expand it to find your tutorial beneath it. Right-click the tutorial and select `Start Didact tutorial`.

## Next Steps

From here, you can add to your new Didact file, create and register other files, and so on!
