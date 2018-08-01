# Container Images using LXD
With LXD, containers are created from an image file. We can take this one step further by configuring a basic container with an OS and the photon environment setup, then subsequently saving a snapshot of this configured state. Using this preconfigured image, we can automate the time-consuming process of building and configuring containers to further accelerate the development experience.

### Prerequisites
+ [photon environment](https://gitlab.acceleratefoundation.io/root/photon)
+ [LXD/LXC](https://linuxcontainers.org/lxd/getting-started-cli/)

### Build a Container
Clone the base repository and navigate to the root directory:
```
git clone https://gitlab.acceleratefoundation.io/root/base-container.git
cd base-container
```
Create a container:
```
photon container --create
```
This command will:
+ create and start a new lxc container named `base`
+ download the latest version of the specified OS & install OS dependencies
+ install command line tools needed to configure photon
+ clone photon and install photon dependencies
+ run photon environment setup

### Create a Container Image
Now that you have created a container, confirm it is running:
```
lxc list
```

Pause the container process:
```
lxc stop base --force
```

Take a snapshot of the container and pass in a name as an alias for your image:
```
lxc publish base --alias=base --force
```

Verify your image was created:
```
lxc image list
```

Remove the old container:
```
lxc delete base --force
```

Now you are free to use photon to clone the local base image and rapidly mount containerized, fully functional apps. 
