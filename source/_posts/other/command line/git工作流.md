#Git operation
Put your project into remote warehouse
1.you need a project code and a code repository(gitHub or coding)

2.initialize local repository
$ git init

3.add the project code to working tree
$ git add .

4.commit your project code
$ git commit -m "first commit notes"

5.synchronize the code to the remote repository
$ git remote add origin your remote reposiroty address

6.create an upstream push to the master branch
$ git push -u origin master

7.now you can create a new dev branch based on the master,and then create your branch based on the dev,keep the developments
Submit code steps

1.add your code to the working tree
$ git add .

2.commit your code
$ git commit -m "notes"

3.pushed to the remote branch
$ git push origin yourBranch

4.switch to the dev branch
$ git checkout dev

5.synchronize remote dev branch code
$ git pull

6.merge your branch code into dev
$ git merge --no-ff -m "merge: notes"

7.pushed to the remote branch
$ git push

8.switch to your branch
$ git checkout yourBranch

9.rebase the dev branch
$ git rebase dev

10.pushed to the remote branch
$ git push origin yourBranch


Resolve git conflict
Merge conflict
1.find the conflict file
2.find the text like this

<<<<<<< HEAD  -- dev branch
 dev code
=======
your code
>>>>>>> 6853e5ff961e684d3a6c02d4d06183b5ff330dcc  -- your branch


3.remove the conflict flag, leaving only one branch of the code (dev code or your code)

4.add changes to the working tree

$ git add .

5.commit your code
$ git commit -m "notes"

6.push changes to dev branch
$ git push

Rebase conflict
1.find the conflict file
2.find the text like this

<<<<<<< HEAD  -- dev branch
dev code
=======
your code
>>>>>>> 6853e5ff961e684d3a6c02d4d06183b5ff330dcc  -- your branch


3.remove the conflict flag, leaving only one branch of the code (dev code or your code)

4.add changes to the working tree
$ git add -u
5.continue rebase
$ git rebase --continue
6.until all conflicts resolved
7.if you want to quit rebase
$ git rebase --abort

attention: after rebase,don`t need to commit and submit new changes,all git automatically

### STS ###
.apt_generated
*.classpath
.factorypath
*.project
*.settings/
*.springBeans
*.class

### IntelliJ IDEA ###
*.jar
# *.war
*.ear
*.log
*.mvn

*.idea
*.iws
*.iml
*.ipr

target
src/test

### NetBeans ###
nbproject/private/
build/
nbbuild/
dist/
nbdist/
.nb-gradle/
need to remove cached first :

1
git rm -r --cached .



