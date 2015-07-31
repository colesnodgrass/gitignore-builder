# gitignore-builder

Combines multiple [GitHub hosted gitgnore files](https://github.com/github/gitignore) into a single local .gitignore
file.  Also supports manually recreating the .gitignore file in the event that the GitHub hosted files were changed.

I grew tired of having to manually combine multiple _recommended_ gitignore files into a single project specific one
and then having to maintain it anytime a new language was added to a project.  This code solves that problem.

## Installation
For me it's easiest to symlink this script into my local ~/bin directory, assuming your ~/bin directory is part of
your $PATH.
```bash
$ git clone git@github.com:cole-snodgrass/gitignore-builder ~/src/gitignore-builder
$ ln -s ~/src/gitignore-builder/gitignore-builder ~/bin/
$ gitignore-builder -h
usage: gitignore-builder [-h] [-u] [-v] [ignores [ignores ...]]

combines multiple gitignore files together into a single file

positional arguments:
  ignores        gitignore file to fetch

optional arguments:
  -h, --help     show this help message and exit
  -u, --update   update the existing .gitignore file
  -v, --verbose  verbose output for debugging
```

## Usage
```bash
$ gitignore-builder Java Python Groovy Gradle Windows
found gitignore file for Java
found gitignore file for Python
unable to find gitignore file for Groovy
found gitignore file for Gradle
found gitignore file for Windows
done
```

This created a .gitignore file in whichever directory it was executed in.
```bash
# {"updated": "2015-07-31 12:16:28.336736", "ignores": ["Java", "Python", "Groovy", "Gradle", "Windows"]}
# SUCCESS: Java - https://raw.githubusercontent.com/github/gitignore/master/Java.gitignore
# SUCCESS: Python - https://raw.githubusercontent.com/github/gitignore/master/Python.gitignore
# FAILURE: Groovy
# SUCCESS: Gradle - https://raw.githubusercontent.com/github/gitignore/master/Gradle.gitignore
# SUCCESS: Windows - https://raw.githubusercontent.com/github/gitignore/master/Global/Windows.gitignore

### Java begin
*.class

# Mobile Tools for Java (J2ME)
.mtj.tmp/

# Package Files #
*.jar
*.war
*.ear

### ... rest of file ...

# Recycle Bin used on file shares
$RECYCLE.BIN/

# Windows Installer files
*.cab
*.msi
*.msm
*.msp

# Windows shortcuts
*.lnk

### Windows end
```

To update an existing .gitignore file that was created with this script
```bash
$ gitignore-builder -u
will attempt to update the following gitignores: Java, Python, Groovy, Gradle, Windows
found gitignore file for Java
found gitignore file for Python
unable to find gitignore file for Groovy
found gitignore file for Gradle
found gitignore file for Windows
done
```
