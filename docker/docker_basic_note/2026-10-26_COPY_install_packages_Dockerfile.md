<h1>Install packages for Dockerfile</h1>
To install required packages for a Dockerfile, you need to check the projects files to what out what a Dockerfile needs to install.

1. Check if there are any dependency files.
EXAMPLES
```console
PYTHON: requirements.txt, pyproject.toml, setup.py, Pipfile
NODE: package.json (and package-lock.json)
GO: go.mod
JAVA: pom.xml, build.gradle
RUBY: Gemfile
RUST: Cargo.toml
```
2. The README and docs
Look for "installations", "prerequisites", or "requirements" sections. They often has system level packages that manifest files don't over (like ffmpeg, libzmq, or git).

3. Existing build and setup scripts
Look at Makefile, setup.sh, install.sh, docker-compose.yml, CI congifs (.github/workflows/*.yml).* 
CI files are useful because they shows what a clean machine needs to build and run the project. 

CI (Continuous Integration Configuration File) is a text file placed in a software project's repository that automates how code is built, tested, and validated.

CI (such as .gitlab-ci.yml) or workflow file in GitHub Actions) tells an automation server what steps to execute whenever a dev pushes new code. 

It defines stages like building, running unit tests, linting, and packaging (such as creating a Docker container).

When you push code to a repo, the CI/CD platform reads the file and runs the defined job automatically. If the test fails, the pipeline stops and alerts the team.

4. Read the imports in the source code
If there's no manifest, scan the code for import / require/ #include lines. Anything that isn't part of the standard library is something that needs to be installed.

EXAMPLE
```console
During the repo-viewer project, if there are not requirements.txt file, I will check the .py file, (source code) and locate *import* to see the required packages. I need to install. In my case, it was Requests, and Flask. 
```
5. Just try it and read the errors.
Build the image and run the app; errors tell you what's missing.
```console
ModuleNotFoundError / Cannot find module: a language packages is missing

command not found: a system tool is missing

error while loading shared libraries: libXYZ.so: a system library is missing (install it with apt-get)

Compiler errors during *pip install*: you often need build tools like gcc or -dev headers
```
6. Check what the dependencies themselves need
Some Python or Node packages wrap C libraries and need system packages first. The package's PyPI/npm pages or docs usually list (for example, pyzmq can often install from a wheel, but some packages need libzmq-dev).

7. Look at the environment that project was built on
If the project works on someone's machine, pip freeze, pip list, or apt list --installed there shows what's installed. This is often a last resort.


```console
 COPY requirements.txt .
 RUN pip install --no-cache-dir -r requirements.txt
 ```

