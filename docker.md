# A docker primer

A short tutorial on docker

## Set-up

The user needs to belong to the group `docker`. The following command lets you can check this:

    groups username

If the output is something like `username : username docker` you are good to go. It means that the user is part of the
groups `username` and `docker`. (A group with the same name as the user is always created while creating the user.)

If you do not belong to the group `docker`, consult your system admin. Basically, this is the person with the `sudo`
privilages on your server. You will be added to the `docker` group with the command below [ref](https://askubuntu.com/questions/79565/how-to-add-existing-user-to-an-existing-group):

    sudo usermod -aG docker username

`-a` means to append the group (`docker` above) to the list of groups a user is associated with
`-G` means a comma separated list of groups (none above)

## Pulling a docker image

You will need the _"pull"_ a `docker image` (basically a template) and then start a `docker container` based on the
pulled image.

Pulling the image:

    v2.9.3: Pulling from comparative-genomics-toolkit/cactus

You can inspect pulled/downloaded images with the following code:

    docker image ls

The output of `docker image ls` would be something like the following:

    REPOSITORY                                    TAG       IMAGE ID       CREATED        SIZE
    quay.io/comparative-genomics-toolkit/cactus   v2.9.3    6edb410ba0e5   3 months ago   1.03GB
    broadinstitute/gatk                           4.1.3.0   0ef3d00baa09   5 years ago    3.72GB

When you start a `docker container` out of a `docker image`, you will have an isolated environment that is separated
from the host, this is by design. In some cases though, you will want to use some data from the host (i.e. FASTQ files).
You can start a container and at the same time attach a local folder to the container with the following code:

    docker run --name alias_for_the_container -it -v full_path_of_the_folder_within_host:mount_point_within_the_container docker-image-to-be-used

- `--name`: a name for the container to be created
- `it`: the container is started with the interactive mode so you can work within it
- `-v`: used to mount/bind a folder from the host to the container

The easiest is to navigate to the folder of interest in you host machine and run the `docker run ...` command there:

    docker run -it -v ./:/data/ quay.io/comparative-genomics-toolkit/cactus:v2.9.3
    
Do not forget to specify the `TAG` at the end.
