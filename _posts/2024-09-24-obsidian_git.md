
[The Easiest Way to Setup Obsidian Git (to backup notes)](https://forum.obsidian.md/t/the-easiest-way-to-setup-obsidian-git-to-backup-notes/51429)
Share & showcase
Jan 2023
19d

ithinkwong
Jan 2023
I watched a few videos on how to setup the obsidian-git plugin and it feels like most of them overcomplicate the process. So I decided to write a set of instructions and a video to show how easy it to accomplish this even if you have no idea what “git” is.

By the end of this tutorial, you will be able to sync your notes from Obsidian to Github for free!

The Easiest Way to Setup Obsidian Git (4 Minutes)
The Easiest Way to Setup Obsidian Git (4 Minutes)
Create a repository or fork the md repo 3.3k in github
Download Git 1.4k
Create a personal access token 2.7k from githubcreate-pat-github.png
Install the Obsidian Git 4.4k community plugin
Create a folder to store the repository. (e.g. remote-blog/). Set scopes to repo & expiration to no expiration
Run the command (CMD/Ctrl + P): Clone an existing remote repo clone-repo-git-plugin.png
Paste the URL of the forked repository in the following format
https://<PERSONAL_ACCESS_TOKEN>@github.com/<USERNAME>/<REPO>.git
For example it might look like this:

https://ghp_XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX@github.com/ithinkwong/linked-blog-starter-md.git
Then type in the folder you created in step 5 (e.g. remote-blog/)
Restart Obsidian
Make edits to your notes
Publish your notes run the command “Obsidian Git: Create backup” by opening the command palette (CMD/Ctrl + P)
