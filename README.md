# git-tutorial

Login to the AWS EC2 node as user `devops`:
```
$ ssh devops@IP-ADDRESS
```

Once logged in you will be in /home/devops.

Clone the Git repo `docker-java-sample` there:
```
$ git clone https://github.com/kurianinc/docker-java-sample.git
```
This will clone the repository under the directory `docker-java-sample`. If needed, default directory name can be changed.

Under `docker-java-sample` directory, build the Java app:
```
$ cd docker-java-sample
$ mvn package
$ mvn exec:java
```

You will see `Hello World!` printed among the deluge of build output.

Now try to make some change to the source code file where the above message printed.

Prior to making the change create a feature branch for the changes that you plan.

Check active branches locally:
```
$ git branch
* master
```

Create a new branch `tk-change-message` off the current branch `master`, and, make that current:
```
$ git branch tk-change-message
$ git checkout tk-change-message
```

Edit the source file to make changes:
```
$ vi src/main/java/org/examples/java/App.java
```

Commit the change to Git locally:
```
$ git commit src/main/java/org/examples/java/App.java -m "Updated message"
```

Push the committed changes to Git server:
```
$ git push --set-upstream origin tk-change-message # First time after the branch is created
$ git push # Subsequent code pushes to remote server
```

The user credentials to access Git server can be cached locally so you won't be prompted for those when code is pushed.

```
$ git config --global credential.helper 'store --file ~/.git-creds'
```
