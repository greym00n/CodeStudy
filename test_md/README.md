# FastDDS (Open-source)
- [Link](https://github.com/eProsima/Fast-DDS)
- [Linux installation from sources](https://fast-dds.docs.eprosima.com/en/latest/installation/sources/sources_linux.html)   
There are two options for installation: (1) using docker and (2) building from the source.

## Install using docker 
1. Download docker container image from [here](https://www.eprosima.com/index.php/products-all).  
It may require sign-in.   
If you have an issue in sign-in, use my downloaded file [here](https://drive.google.com/file/d/1HWA3HtUTRzZTBLRTSPfsUrWhmHLk6pPM/view?usp=share_link).
![](https://i.imgur.com/HMBOBu1.png)
![](https://i.imgur.com/kq9boO3.png)

2. Load the docker image:   
`docker load -i ubuntu-eprosima-dds-suite\ v1.3.0.tar`
![](https://i.imgur.com/tPEzWPi.png)


### Basic example (Helloworld)
1. Run Docker container   
`docker run -it ubuntu-eprosima-dds-suite:v1.3.0`
2. Run the example
    - Go to examples folder  
    `goToExamples`
    `cd dds/HelloWorldExample/bin`
    ![](https://i.imgur.com/8ygcVPQ.png)
    - Run helloworld  
    `tmux new-session "./DDSHelloWorldExample publisher 0 1000" \; \
         split-window "./DDSHelloWorldExample subscriber" \; \
         select-layout even-vertical`
            ![](https://i.imgur.com/qiw0pnM.png)

## Building from source
[Original instruction from webpage](https://fast-dds.docs.eprosima.com/en/latest/installation/sources/sources_linux.html#colcon-installation)
- Dependencies  
    `sudo apt install cmake g++ python3-pip wget git`  
    `sudo apt install libasio-dev libtinyxml2-dev`  
    `sudo apt install libssl-dev`  
    `sudo apt install libp11-dev libengine-pkcs11-openssl`  
    `sudo apt install softhsm2`  
    `sudo usermod -a -G softhsm <user>`  
    `sudo apt install libengine-pkcs11-openssl`  
    `p11-kit list-modules` # for check  
    `openssl engine pkcs11 -t` # for check  
    `git clone https://github.com/google/googletest src/googletest-distribution`  
- Colcon installation  
    `pip3 install -U colcon-common-extensions vcstool`  
    `mkdir ~/Fast-DDS`  
    `cd ~/Fast-DDS`  
    `wget https://raw.githubusercontent.com/eProsima/Fast-DDS/master/fastrtps.repos`  
    ![](https://i.imgur.com/3zgU7CW.png)  
    `mkdir src`  
    `vcs import src < fastrtps.repos`  
    ![](https://i.imgur.com/yKnT3dN.png)  
    `colcon build`  
    ![](https://i.imgur.com/kOwg1AY.png)  
- Sourcing  
`source ~/Fast-DDS/install/setup.bash`  
`echo 'source ~/Fast-DDS/install/setup.bash' >> ~/.bashrc`  
### Basic example (Helloworld)
- Go to example folder  
`cd src/fastrtps/examples/cpp/dds/HelloWorldExample`  
`cmake .`  
`make`  
You will see DDSHellowWorldExample bin file.
- Run pub sub exam
    - Terminal #1: publisher  
    `./DDSHelloWorldExample publisher`  
    ![](https://i.imgur.com/2VB2AFs.png)  
    - Terminal #2: subscriber  
    `./DDSHelloWorldExample subscriber`  
    ![](https://i.imgur.com/Btl8nSf.png)  


# CycloneDDS (Open-source)
- [Link](https://github.com/eclipse-cyclonedds/cyclonedds)
## Install
- Clone  
`git clone https://github.com/eclipse-cyclonedds/cyclonedds.git`  
- Build  
`cd cyclonedds`  
`mkdir build`  
`cd build`  
`cmake -DBUILD_EXAMPLES=ON -DBUILD_TESTING=ON ..`  
If you want to install CycloneDDS in specific folder, use `-DCMAKE_INSTALL_PREFIX=<install-location>`.  ([more configuration](https://github.com/eclipse-cyclonedds/cyclonedds))  
`cmake --build . --target install`  
This may require administrative privileges.

## Basic example
### Helloworld
As you used `-DBUILD_EXAMPLES=ON`, they are already compiled (you don't need to compile examples in `example` folder).
- Subsciber  
`./HelloworldSubscriber`  
![](https://i.imgur.com/A0zlgp3.png)
- Publisher  
`cd bin`  
`./HelloworldPublisher`  
![](https://i.imgur.com/J9MiftC.png)



# RustDDS (Open-source)
- [Link](https://github.com/jhelovuo/RustDDS)
## Install
- Clone  
    `git clone git@github.com:jhelovuo/RustDDS.git`
- Build  
    It requires [cargo](https://doc.rust-lang.org/cargo/getting-started/installation.html). I tested this using cargo 1.61.0.  
    `cargo build`
## Basic example

### Shape demo
- Subscriber using Rust DDS  
  This example is for validation of interoperability between different DDS.  
`cd exmaple/shapes_demo`  
`run cargo run --example=shapes_demo -- -S -t Square`  
It will compile files for a while if it is the first time.  
![](https://i.imgur.com/n52zieu.png)  
Then you will see Subscriber is activated.  
![](https://i.imgur.com/QR5SwZK.png)  
- Publisher using another DDS (e.g., FastDDS)  
You will see Subscriber is taking the topics (e.g., Squares).  


---
# CoreDX DDS (**Not** open-source)
- [Link](http://www.twinoakscomputing.com/coredx/download)
## Installation
- After you register it, CoreDX license manager will send a license file.
  - You need to use your university email address (they will require).
  - It takes 1~2 business day usually.
- Download CoreDX DDS from the webpage.
![](https://i.imgur.com/q1K4MFj.png)
- Place license file in your folder and set `TWINOAKS_LICENSE_FILE` to your license file location.  
`export TWINOAKS_LICENSE_FILE=LICENSE_FILE` 
## Basic example (helloworld)
- Go to example folder   
`cd examples/hello_c`  
- Set `COREDX_TOP`, `COREDX_HOST`, `COREDX_TARGET` to your own directory for `Makefile`.  
`make`  
- Run pub-sub example 
  - Terminal #1: Publisher  
`./hello_pub`
  - Terminal #2: Subsriber  
`./hello_sub`


# GurumDDS (**Not** open-source)
- [Link](https://gurum.cc/)
## Installation  
![](https://i.imgur.com/y9zpTVV.png)  
![](https://i.imgur.com/p9Qs7ha.png)  
It will give you temporary password and liscense through the email.  
Download zip file and extract under your folder (e.g., gurumDDS)  
`cd gurumDDS`  
`make`  
## Basic example
- go to example folder  
`cd examples/helloworld`  
- Terminal #1: Publisher  
`./publisher`  
![](https://i.imgur.com/NMCuK7v.png)  
- Terminal #1: Subscriber  
`./subscriber`  
![](https://i.imgur.com/qHqNRTG.png)  

---
OpenDDS and RTIconnexDDS are omitted.