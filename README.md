# Project Vexriscv Ruffle Axi
##  Target: Nexys A7-100T(DDR)

---

  author: Jay Convertino

  date: 04/03/24

  license: MIT

---

Requirements:

  * Ubuntu 20.04 or greater.
  * Vivado 2022.2.2 or greater.
  * Fusesoc 2.4 or greater.
  * sbt version 1.9.8
  * Java version 17.X

  <div style="page-break-after: always;"></div>

### Document Version
* v0.0.0 - 04/03/24 - Initial document, needs testing.

#### Document History
* NONE

  <div style="page-break-after: always;"></div>

#### Folders
  * cfg, contains openocd configurations.
  * deps, contains binaries needed for build.
  * hdl, contains IP cores for FPGA fusesoc build system.
    * hdl/build/AFRL_project_ruffle_axi_linux_1.0.0/nexys-a7-100t-vivado/ contains the vivado project files.
  * sw, contains software and tools for Ruffle CPU.

#### Git Stuff

To pull all submodules use the following:
  * git submodule update --force --init --recursive

### Setup Ubuntu Packages

1. In a terminal, enter the following command to install required packages:

      ```
      sudo apt-get install build-essential python3-pip python-is-python3 \
      autoconf automake autotools-dev libmpc-dev libmpfr-dev gawk bison flex \
      texinfo gperf libtool patchutils ninja-build git cmake libglib2.0-dev \
      libusb-1.0-0-dev libusb-dev libyaml-dev libncurses5 libtinfo5 \
      openjdk-17-jre-headless minicom putty
      ```

      - The above will install all the needed dependencies in Ubuntu

2. Next enter the command below to install python required packages:

      ```
      pip install GitPython fusesoc
      ```
      - The above will install the fusesoc hdl build system.

    <div style="page-break-after: always;"></div>

### Install sbt tool

0. Launch your file manager (nautilus) and navigate to the ace_vexriscv_murax folder.
1. In the root of the ace_vexriscv_murax folder navigate to the deps folder.
2. Enter the folder and look for the tar file `sbt.tar.gz`
3. Launch a terminal by right clicking in the folder and selecting `launch in terminal`.
    - Or navigate using cd command in terminal.
4. Extract `sbt.tar.gz` to your user .local/bin folder using the following command.

      ```
      tar -zxf sbt.tar.gz -C ~/.local/ --strip-components=1
      ```
      - The above will extract sbt to the local bin folder where fusesoc resides.

  <div style="page-break-after: always;"></div>

### Vivado

1. If Vivado is not installed, download and follow the instructions to install Vivado only. Vitis is not needed.
2. Install location does not matter, but Vivado install is performed by the local user NOT root.
3. The apt-get command in `Install Ubuntu Packages` takes care of the needed dependencies for Vivado, you're welcome.

  <div style="page-break-after: always;"></div>

### Setup local PATH

1. In a terminal, execute the following to start editing the user bashrc.

    ```
    nano ~/.bashrc
    ```

2. In nano add the following lines to bashrc

    ```
    PATH=/home/$USER/.local/bin/:$PATH
    PATH=/your/path/to/vivado/bin/:$PATH
    ```

3. Save file and exit nano.
4. Execute source command if using same terminal session to kick-off build.

    ```
    source ~/.bashrc
    ```

  <div style="page-break-after: always;"></div>
