# What is repo
Repo is a system for using different "git" projects together.

## Installation
+ Install "repo" for linux.

```
 sudo apt-get install repo
```
## Use Repo
+ **Step 1 :** Repo Initialization
```
 repo init -u https://github.com/KMACEL/Examples-Repo.git -b master -m default.xml
```



| Parameter     | Description   |
| ------------- |:-------------:|
| -u            | This is the parameter used to give the link (url) with the "git" extension in which the repon is located.  |
| -b            | The parameter used to give the name "branch" to be used in the repo. Default Value : master      |
| -m            | The parameter used to give the name of the manifest file of the repo (I'll tell you soon). Default Value : default.xlm      |

+ **Step 2 :** Repo Synchronization
```
 repo sync
```
It does give repo data according to the manifest file in the repo init process

## Create New Manifest
+ Manifest files tell what repo commands will do. It is written in "XML" format.

Examples ;

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <remote name="origin" fetch="https://github.com/KMACEL"/>
  <default revision="master" remote="origin" />

    <project path="apps/IITR" name="IITR" remote="origin" />
    <project path="apps/gogenux" name="gogenux" remote="origin" />
</manifest>
```

+ **Remote :** Reports the location of the project. A lot of "remote" can be added.
```xml
<remote name="origin" fetch="https://github.com/KMACEL"/>
```

+ **Default :** If an external "remote" is not given to the project, the settings specified here will prevail.
```xml
<default revision="master" remote="origin" />
```

+ **Project :** The repo sync process is performed on a project basis.
  + **path :** When Repo Sync is done, it tells which folder structure the future project will be in
  + **name :** In the main project file that is given to remote, it informs which project to take.
  + **remote :** Tells which project master file to import.

  ```xml
  <project path="apps/IITR" name="IITR" remote="origin" />
  ```

## Working Branch
+ You can provide multiple forms of work in a repo project. This is done by defining a branch in each new manifest file and, when the branch is changed in the ".repo / manifests /" directory in the folder for the other project, the command "repo sync" is given to repo according to the new branch manifest.

+ Examples;
```
cd .repo/manifests/
```
```
git checkout global
```
```
repo sync
```

## Repo Command
+ In large projects, for example when using a repos for an "OS", there are some commands that will help us. Let's examine them now.

### Repo Forall
+ This command saves lives in real sense. Thanks to this command, all ".git" projects in the repo can be processed at the same time.
+ Examples ;
```
repo forall -c "ls -al"
```
  + This is a very simple example. But you can write any command you want to run between -" "-. This can be a "bash" command, a "git" command, or any executable file.

### Repo Status
+ This command tells us about "git" projects in the repo, "do you have new files?", "Do you have new commit?" . In a nutshell, it goes back into every "git" project and returns "git status" as if it had been written.
```
repo status
```

### Repo Upload
+ If a project has a "url" if it will perform a review, that is, it supports it, then after making the change "commit" it sends this command directly to the review process.
```
cd apps/IITR
```
*change main.go*
```
git add main.go
```
```
git commit -m "Change main.go"
```
```
repo upload .
```

### Repo Start
+ After the repo sync process, not all projects have any branch tees. In this command, all projects can be brought to the same branche.
```
repo start master
```

## Reference Links

| Links     |
| ------------- |
|https://source.android.com/setup/downloading|
|https://source.android.com/setup/using-repo|
|https://source.android.com/setup/downloading|
|https://source.android.com/setup/developing|
|https://forum.xda-developers.com/android/software/guide-android-repo-mirroring-t3170869|
|https://www.excentral.org/archives/2011/02/24/android-repo-mirroring|
|https://groups.google.com/forum/#!topic/repo-discuss/lS34iKQtxiY|
|https://groups.google.com/forum/#!topic/repo-discuss/nzPN9dczEus|
|https://nativeguru.wordpress.com/tag/repo-mirror/|
|http://bhundven.blogspot.com.tr/2013/06/master-of-android-repo-mirrors.html|
|https://github.com/yasuaki/repo-help-ja/blob/master/repo-init.txt|
|http://blog.udinic.com/2014/05/24/aosp-part-1-get-the-code-using-the-manifest-and-repo/|
|https://dev.vaadin.com/review/Documentation/user-upload.html|
|https://wladimir-tm4pda.github.io/source/git-repo.html|
|https://stackoverflow.com/questions/20921673/create-android-server-local-repository-for-specific-tag|
|https://stackoverflow.com/questions/19530585/pushing-repo-branch-to-local-aosp-mirror|
