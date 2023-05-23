## Git to Debian 


Installing Git to Debian 11:Also remember to create a new repository to Github.  

     git --version
     -> bash: git: command not found

     sudo apt-get update
     sudo apt install git

     git --version
     ->
     git version 2.30.2

     git init

     git status      
     -> On branch master
     No commits yet

     Untracked files:
     (use "git add <file>..." to include in what will be committed)
	   db.sqlite3
	   kesadjango/
     manage.py
     people/
     todo/  
  
    git add .

    git status

    git commit -m "first commit"
    
    (If you haven't created a repository on github yet, create it now)
  
    git remote add origin https://github.com/githubusername/REPOSITORY.git
        
    git push -u origin master

    Username for 'https://github.com': Give you github username	
    Password for 'https://githubusername@github.com': 
    remote: Support for password authentication was removed on August 13, 2021.
    remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of 	authentication.
    fatal: Authentication failed for 'https://github.com/githubusername/REPOSITORY.git/'
    
    --> go to github and create a token
        --> settings > Developer Settings > Personal Access Tokens > Tokens (Classic) > Generate New Token > Generate New Token (Classic) 

And again:  

    git push -u origin master

    Username for 'https://github.com': Give you github username	
    Password for 'https://githubusername@github.com': paste here the token you copied from Github

    -->
    Enumerating objects: 62, done.
    Counting objects: 100% (62/62), done.
    Delta compression using up to 3 threads
    Compressing objects: 100% (59/59), done.
    Writing objects: 100% (62/62), 18.50 KiB | 1.68 MiB/s, done.
    Total 62 (delta 13), reused 0 (delta 0), pack-reused 0
    remote: Resolving deltas: 100% (13/13), done.
    To https://github.com/githubusername/REPOSITORY.git
     * [new branch]      master -> master
    Branch 'master' set up to track remote branch 'master' from 'origin'.

