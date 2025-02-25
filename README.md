# freecad_commandline
Making the dream of many come true. Command line

### Installing this plugin is as simple as downloading the file .FCMacro from this repo, placing them in your freecad macros folder, and running it.

I definitely decided that the translated command file was the best option, so I didn't have to load each workbench to have all the commands available in freecad.
Again the installation method is:
- Download the .FCMacro file and the commands.json file from the folder of the required language
- Place both files in the freecad macros folder or your preferred folder

### To use it:
- Run the macro
- Press the Esc key: this will always focus the text box every time you want to write the name of the command globally, the only thing that intervenes when using freecad by default is that it does not deselect all the elements.
- Write the approximate name of the required command
- You can navigate with the up and down arrows until you find the desired one, then press enter. The command is executed
- If you want to reuse the commands used, without typing any suggestion you can press the down arrow, and the last 4 commands used will appear


### To contibute it:

Execute this command in python console with all workbenches pre-loaded:

```
all_commands = []
commands = FreeCADGui.listCommands() 
for cmd_name in commands:
    cmd = FreeCADGui.Command.get(cmd_name)  
    if cmd:
        actions = cmd.getAction()  
        if actions:
            if isinstance(actions, list):  
                action = actions[0] if actions else None
            else:
                action = actions  
            
            if action:
                menu_text = action.text()  
                print('{'+f'"type":"{cmd_name.split("_")[0]}","command":"{cmd_name}", "name":"{menu_text.translate({ord("&"): None})} ({cmd_name.split("_")[0]})"'+'},')  
                all_commands.append({"name": f"{menu_text.translate({ord('&'): None})} ({cmd_name.split('_')[0]})","command":cmd_name})```


Make a new json file with the output and set name "commands.json" in new folder of your language.
publish your language by making a pull request.
