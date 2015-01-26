## Suggested Workflow

Since many of you are new to the concept of Virtual Machine (VM), Docker, and
Git, I will outline here how I would go about doing the assignments if I were running Boot2Docker on Windows or OS X. The problem here is that almost every assignment in this course will have an IPython notebook template on GitHub INFO490 repsitory, 

https://github.com/INFO490/spring2015

and you **must** use these templates on your notebook server. In the following,
I will describe how to use Git to download the templates and use them on your
IPython notebook server.

However, do note that I run Linux exclusively for everyday use, and my suggestion descrbed in the following may not be the optimal one. If you can think of a better way to use the IPython templates on the course repository, you may do it your way as long as you use the provided templates. But also note that you **must** use the course Docker image; installing and running IPython on Windows or OS X is **not** acceptable and may result in a zero for the assignment.

In the following, I will assume that you have [Folder Sharing](https://github.com/INFO490/spring2015/blob/master/week00/docker_folder_sharing.md) enabled and use [Problem 3.1](p1.md) as an example.

If your data volume named `my-data` is mounted at `/data`, run a terminal with
the data volume mounted in the container:

```console
$ docker run --rm -it --volumes-from my-data lcdm/info490 /bin/bash
```

Here, by specifying ``--rm`` argument the docker container is automatically
removed when you exit the container. This will give you a command prompt in container. Move to `/data` and run `git clone`:

```console
root@containerID:/notebooks# cd /data
root@containerID:/notebooks# git clone https://github.com/INFO490/spring2015
root@containerID:/notebooks# ls
spring2015
root@containerID:/notebooks# exit

Now your data volume has a copy of the course repository. Note that you run `git clone` only once. Once you have cloned a repository, to update your local copy of the repository, go to the corresponding directory and run

root@containerID:/notebooks# git pull

Now make sure that an IPython notebook server is running (see [Running
Docker](https://github.com/INFO490/spring2015/blob/master/week00/docker_running_ipynb.md)) with your data volume mounted, and
open up your web browser and go to http://192.168.59.103:8888 (the address of
your notebook server may be different). Note that the notebook server shows the
notebooks in `/notebooks` folder, so you will have to move the template from
`/data` to `/notebooks`. There are various ways to do this (Note that simply
doing `cp /data/spring2015/week03/hello.ipynb /notebooks/.` is not one of
them). I'll show you one of them by demonstrating the use of [cell magics in
IPython](http://nbviewer.ipython.org/github/FRidh/ipython/blob/1.x/examples/notebooks/Cell%20Magics.ipynb).

Create a new notebook by clicking on `New Notebook`. In the cell, type

```console
%%bash
cp /data/spring2015/week03/hello.ipynb /notebooks/.
```

and press <kbd>shift</kbd> + <kbd>enter</kbd>. Now a notebook named `hello`
should appear in the lsit of notebooks in your *IPython Dashboard*.

Alternatively, you can download the template from the GitHub webpage, save it
on your host computer, and open this file from your notebook server.