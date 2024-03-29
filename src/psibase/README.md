# Overview

This template allows anyone to start developing new PsiBase web services (frontend and backend) in just a few clicks. When using this template, you will connect VSCode to a preconfigured docker container, generate a project, and deploy your new project to a running instance of Psinode.


# Prerequisites

1. VSCode installed on your development PC
2. Docker desktop is installed on your development PC
3. [Psidekick extension](docker-desktop://extensions/marketplace?extensionId=jamesmart/psidekick&tag=0.1.3) installed in Docker Desktop
4. [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) VSCode extension has been installed.

# Instructions

1. Install VSCode
2. Install Dev Containers extension
3. Run the `Dev Containers: Add Dev Container Configuration Files...` command in VSCode and answer the prompt(s)
4. Run the `Dev-Containers: Rebuild and Reopen in Container` command in VSCode
![](/res/rebuild_reopen.png)

If you don't already have Docker Desktop installed, you should be automatically prompted to install it. VSCode will then relaunch, connecting to a new docker container with an environment pre-configured to be able to build Psibase Services. This can take a few minutes on the first time for it to build the docker container.

Once inside the docker container, open the integrated terminal within VSCode (```Ctrl+Shift+` on Windows```) and run `psi-generate`. Follow the on-screen instructions to generate and open a new project.

You may use the buttons at the bottom of the VSCode window to build & test your project (You can even customize these buttons and their functionality by modifying `.vscode/tasks.json`). Note: Testing functionality is currently disabled.

![](/res/build_test.png)

When you're ready to deploy your project, follow the deployment instructions found [here](https://doc-sys.psibase.io/cpp-service/basic/index.html#deploying-the-service).

*To-do: Use a graphical UI from the chain for deployment.*

# Additional notes

When VSCode closes, the container stops. The data within the container is not accessible, as it's stored in an unnamed volume mounted on your PC, only accessible through the docker container launched by VSCode.

All changes made within the container will persist on your PC (as long as you don't delete the docker volume), and must be pushed to a git repository if you want to work on it on another PC.

## Windows troubleshooting

If you're on Windows, using Docker Desktop with WSL2, it is likely that the WSL2 process will chew up an enormous amount of memory on your PC. The solution is simply to:
1. Shut down docker desktop
2. Run `wsl --shutdown` from a command prompt
3. Create a `.wslconfig` file in `%userprofile%` if it doesn't exist
4. Add the following config to the `.wslconfig` file
```
[wsl2]
memory=6GB
```
5. That's it. Save the file and restart Docker Desktop, and now WSL2 is limited to only consume a maximuim of 6GB.
