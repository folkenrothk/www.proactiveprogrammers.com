# Using GatorGrader

[//]: # (Excerpted from prior docs on GatorGrader and Dockagator)

## Introduction

The projects on this web site integrate the
[GatorGrader](https://github.com/GatorEducator/gatorgrader) tool so that an
emerging proactive programmer can receive rapid feedback in either a GitHub
Actions build or in a Docker container running on their computer. Since each
project on this site overviews the checks that GatorGrader runs, the purpose of
this documentation is to explain how to run GatorGrader in a Docker container
using the [DockaGator](https://github.com/GatorEducator/dockagator) Docker image
that runs [GatorGradle](https://github.com/GatorEducator/gatorgradle) and
ultimately results in performing the checks for a specific assignment.

## Non-Interactive Shell

After installing Docker, you can use the following `docker run` command for your
operating system to start `gradle grade` as a containerized application, using
the [DockaGator](https://github.com/GatorEducator/dockagator) Docker image
available on
[DockerHub](https://cloud.docker.com/u/gatoreducator/repository/docker/gatoreducator/dockagator).
When you run one of these commands you should make sure that you do so in the
"home base" of a project (i.e., the directory that contains the `README.md` with
the summary of the project). To learn how to run GatorGrader in a
non-interactive shell, pick the tab for your computer's operating system!

=== "Windows"

    ```bash
    docker run --rm --name dockagator \
      -v "%cd%:/project" \
      -v "%HomeDrive%%HomePath%/.dockagator:/root/.local/share" \
      gatoreducator/dockagator
    ```

=== "Linux and MacOS"

    ```bash
    docker run --rm --name dockagator \
      -v "$(pwd)":/project \
      -v "$HOME/.dockagator":/root/.local/share \
      gatoreducator/dockagator
    ```

Note that both of these commands reference a "project directory" (specified with
the first `-v` argument and the "cache directory" (given by the second `-v`
argument). The project directory (i.e., the "home base" for a project) should
contain the source code and technical writing for a project and the cache
directory should only contain the files and directories created by DockaGator
and GatorGrader. Further instructions for using and changing these commands vary
depending on the operating system installed on your computer!

!!! note

    === "Windows"

        The Docker command for the non-interactive shell uses the `%cd%` and
        `%HomeDrive%%HomePath%` variables to respectively designate the current
        working directory and the home directory for a user's account. Make sure
        that you create the cache directory inside your home account. If you
        face challenges when using either the `%cd%` variable or the drive
        `%HomeDrive%%HomePath%` variable, you can substitute for them with the
        fully qualified path that serves as the project directory or the cache
        directory. Finally, some terminals on Windows do not support
        multiple-line commands and thus you may need to join each line into a
        single long command instead.

    === "Linux and MacOS"

        The Docker command for the non-interactive shell uses `"$(pwd)"` as the
        project directory and `"$HOME/.dockagator"` as the cache GatorGrader
        directory.  Make sure that you create the cache directory by running the
        command `mkdir $HOME/.dockagator`. If you face challenges when using
        either `"$(pwd)"` or `$HOME`, you can substitute for them with the fully
        qualified path that serves as the project directory and cache directory,
        respectively. If you find it difficult to copy and paste the
        multiple-line command you may join each line into a single long command
        instead.

Here are some additional commands that you may need to run when using Docker:

* `docker info`: display information about Docker's current setup
* `docker images`: show the Docker images installed on your computer
* `docker container list`: list the active images running
* `docker system prune`: remove many types of "dangling" components
* `docker image prune`: remove all "dangling" docker images
* `docker container prune`: remove all stopped docker containers
* `docker rmi $(docker images -q) --force`: remove all docker images

Once you have typed the command for running the non-interactive shell, it will
automatically run the [GatorGrader
tool](https://github.com/GatorEducator/gatorgrader), yielding output for you
should carefully inspect. If GatorGrader's output shows that there are no
mistakes in a project, then your source code and technical writing are passing
all of the baseline checks. However, if the output indicates that there are
mistakes, then you will need to understand what they are and try to fix them by
leveraging your topic knowledge and technical and professional skills!

## Interactive Shell

The Docker command for creating a non-interactive shell will, by default, run
the `gradle grade` command and exit the Docker container. If you instead want to
keep the Docker container open, you need to create an interactive shell!
Regardless of your computer's operating system, running an interactive shell
requires you to add the `-it` flag before the `--rm` flag in the command and the
`/bin/bash` at the end of the command. As before, click on the tab for the
appropriate operating system to see how to run an interactive shell!

=== "Windows"

    ```bash
    docker run -it --rm --name dockagator \
      -v "%cd%:/project" \
      -v "%HomeDrive%%HomePath%/.dockagator:/root/.local/share" \
      gatoreducator/dockagator /bin/bash
    ```

=== "Linux and MacOS"

    ```bash
    docker run -it --rm --name dockagator \
      -v "$(pwd)":/project \
      -v "$HOME/.dockagator":/root/.local/share \
      gatoreducator/dockagator /bin/bash
    ```

Once you have typed the correct command for your operating system, you can run
[GatorGrader](https://github.com/GatorEducator/gatorgrader) in the Docker
container by typing the command `gradle grade` in your terminal. As with the
non-interactive shell, running this Docker command will produce a lot of output
that you should carefully inspect! If GatorGrader's output shows that there are
no mistakes in a project, then your source code and technical writing are
passing all of the baseline checks. However, if the output indicates that there
are mistakes, then you should work to understand what they are and then try to
fix them.

## Upgrading DockaGator

If the maintainers of DockaGator provide a new version of the Docker container
called `gatoreducator/dockagator` and you want to receive it immediately, you
must first delete the existing Docker container on your computer by running the
command `docker rmi gatoreducator/dockagator`. After this command completes, you
can then run the appropriate Docker command for your computer's operating
system, prompting the download of the updated version of the DockaGator image
for a Docker container.

If you attempt to run `gradle grade` in an updated Docker container it is
possible that the command will fail if you previously used GatorGrader with a
Docker container that featured a different version of the Python programming
language. In this situation, you should delete the directories inside of the
`.dockagator/` directory and then again attempt to run the `gradle grade`
command inside of the Docker container. Specifically, you will need to delete
directories in the `.dockagator/` directory that are normally called
`gatorgrader/`, `virtualenv/`, and `virtualenvs/`.

## Next Steps

Before you start to learn more about the professional skills of a proactive
programmer, make sure that you review the
[introduction](./introduction-technical-skills.md) to these technical skills.
Have you become comfortable with, for instance, acting on feedback from others,
giving feedback to your colleagues, and giving feedback to yourself? Make sure
that you continue to practice all of these technical skills, participating in
the [proactive
community](../../../proactive-community/community-connections/) by
sharing your ideas for improving this content and helping others to master each
software tool!
