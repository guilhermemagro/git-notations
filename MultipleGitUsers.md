#How to use multiple users with Git

If you are working with multiple git users, for example, one for personal projects and another for a company.

So it's not a good idea to set a global user because all projects are going to use the same. And It will be easy to make a commit with the wrong user.

## Amend

If it's your case, don't worry. It's not really a problem, because you can amend it with this command.

```bash
git commit --author="First Last <first.last@company.org>" --amend --no-edit 
```

But seriously, how want to do that frequently? No one, for sure. It's a thing to use only in emergency cases.

## Git Config

The first thing that I like to do is change the default core editor from vim to VSCode. It's an optional step.

```bash
git config --global core.editor 'code --wait'
```

And then create two alias to easy access the configurations

```bash
alias gcg="git config --edit --global"
alias gcl="git config --edit --local"
```

The difference between them is that global applies to all the git projects on your machine and local only applies to the current path.

Now we are going to learn how to use a different user for each project.

## Remove Global 👌
This steep is recommended, but also optional. I will prefer not to have a default user for all projects, but it is up to you.

Now we are going to open the global config using the gcg alias or with the git config --edit --global command.

Remove all [credential] and [user] configurations.

## The Hard way 👎
One option is after creating or cloning a repository, set manually the configuration with those commands.

```bash
git config user.name "<user>"
git config user.email "<user@mail.com>"
git config credential.username "<user>"
```

It will be good if you don't have a specific path to which to create or clone the projects, but... it takes too much time and is easy to forget, believe me, moreover you are going to need to repeat the same with each repository that you clone.

## The easy way 👍
We are going to define a path where our projects are going to live and create a .gitconfig file for each user profile, as many as we need.

```
~
├── .gitconfig <-- global
└── Developer/
   ├── personal/
   │   ├── project_1/
   │   ├── project_2/
   │   ├── project_#/
   │   └── .gitconfig <-- personal
   └── company/
       ├── project_1/
       ├── project_2/
       ├── project_#/
       └── .gitconfig <-- company
```

## Personal

```
# ~/Developer/personal/.gitconfig

[credential]
    username = <github-user>
[user]
    name = <github-user>
    email = <github-user>@users.noreply.github.com
```

## Business

```
# ~/Developer/company/.gitconfig

[credential]
    username = <user>
[user]
    name = <First Name and Last Name>
    email = <user>@company.org
```

## Global
Now we are going to open the global config using the gcg alias or with the git config --edit --global command.

```
# ~/.gitconfig

[includeIf "gitdir/i:~/Developer/personal/"]
    path = ~/Developer/personal/.gitconfig

[includeIf "gitdir/i:~/Developer/company/"]
    path = ~/Developer/company/.gitconfig
```

So, it will take the user configuration profile per path, and you can create or clone projects inside each profile path without dealing with manual configurations and avoid using the amend command to fix mistakes.