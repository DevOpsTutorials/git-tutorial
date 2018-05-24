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

Make sure that your change is error free and working before a commit:
```
$ mvn package
$ mvn exec:java
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

On the browser, see your branch listed at `https://github.com/kurianinc/docker-java-sample/branches`.

Create a new PR by clicking on the `New pull request` button against your branch.

A PR is essenatially a merge between two branches, usually a merge of feature branch into the parent branch it based on. In this sample case, merging `tk-change-message` into `master`.

A PR is reviewed and approved by team members prior to merging.

Common practices, usually called Git Flow:
- A repo will have branches `master` and 'develop`, `master` representing code in production and `develop` representing ongoing development work.
- Feature branches are created off `develop` and those will be merged into `develop` after testing.
- Prior to pushing code to production, `develop` is merged into `master`.
- For hot-fixes in production branches are created off `master` and merge such changes into both `develop` and `master`.



