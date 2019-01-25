[original article at the CS225 UIUC website](https://courses.engr.illinois.edu/cs225/sp2019//guides/own-machine/)
# Remote Connect
You have two options for remotely working on the EWS Linux cluster:

Running a full desktop session using FastX: https://it.engineering.illinois.edu/user-guides/remote-access/connecting-ews-linux-fastx
* Connecting to a console session over SSH: https://it.engineering.illinois.edu/user-guides/remote-access/accessing-linux-terminals-remotely-ssh
* For Mac OS X or any other Unix-like variant, you will need to open a terminal session.
    * On OS X:
        1. Goto ``Applications->Utilities->Terminal``.
        2. Run the command: ```ssh NETID@linux.ews.illinois.edu (replacing NETID with your NetID)```
        3. If this is your first connection, it will then prompt you to accept the public key from the host; type yes at this prompt and hit enter.
        4. At this point you should be prompted for your AD password; note that you will not see any characters displayed as you type.
        5. If your password was successfully accepted you should have a fully functioning EWS shell.
    * For Windows
    1. Download PuTTY from http://the.earth.li/~sgtatham/putty/latest/x86/putty.exe.
    2. Once you download PuTTY you will be prompted to enter the address to the server. Use ``NETID@linux.ews.illinois.edu``, substituting in your NetID.
    3. You can save this by clicking the save button to the right of the highlighted default session. Optionally you could name this connection EWS.
    4. Now click connect and click “Yes” if it prompts you to accept the public key of the host machine.
    5. You will be asked to enter your AD password; note you will not see any characters as they are typed.
    6. If your password was successfully accepted you should have a fully functioning EWS shell.
**We recommend** connecting to a console session since an excessive amount of FastX sessions tends to become unstable on the EWS cluster or ends up refusing connections.

# Working Natively
### Windows
The Windows Subsystem for Linux (WSL) is an amazing tool allowing Linux to run in Windows natively. To get WSL installed:
1. Follow Microsoft’s instructions for installing WSL, choosing Ubuntu as the distribution: https://docs.microsoft.com/en-us/windows/wsl/install-win10.
2. Continue following Microsoft’s instructions for initializing your Ubuntu distribution: https://docs.microsoft.com/en-us/windows/wsl/initialize-distro

3. Download the packages used for C++ by running the following command to install the packages we will be using:
$
    ```
    sudo apt-get update && sudo apt-get install clang-6.0 libc++abi-dev libc++-dev git gdb valgrind graphviz imagemagick gnuplot cmake
    sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-6.0 100
    sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-6.0 100
    sudo update-alternatives --install /usr/bin/llvm-symbolizer llvm-symbolizer /usr/bin/llvm-symbolizer-6.0 100
    ```
#### Using your Windows Desktop in WSL/Ubuntu
When you start Ubuntu, your shell will begin in the Linux home directory. However, you will likely want to work with files that are somewhere inside of your Windows file system. By default, your ``C:`` drive is mounted at ``/mnt/c``.

Some find it useful to create a shortcut to jump directly to your Windows Desktop (or possibly a cs225 folder inside your Windows desktop). To do so:

1. Navigate to your Windows desktop within the Linux shell:
$
    ```
    cd /mnt/c/Users/
    cd <Your-User-Name-on Windows>  // Use `ls` to find the available users in green
    cd Desktop
    ```
2. In your Windows Desktop directory you just navigated to, run the following command to create a symbolic link (ex: a shortcut) from your Linux home directory to your Windows desktop to easily navigate there in the future:
$
    ```
    ln -s `pwd` ~/desktop
    ```
3. In the future when you launch WSL/Ubuntu, you can immediately jump to your Windows desktop by running ``cd desktop``.
### Linux
You should make sure you have the following packages installed:

* [Clang](http://clang.llvm.org/) and [libc++](http://libcxx.llvm.org/) and the libc++abi: The Clang compiler and the libc++ C++ standard library implementation. This provides all of the compiler Utilities. On most distros you will need to make sure you have ``clang``, ``libc++`` and ``libc++abi`` (or similar) packages installed.
* [Valgrind](http://valgrind.org/): A tool for finding memory leaks and general programming errors.
* [Graphviz](http://www.graphviz.org/): Graph plotting tools used for assignments which display graphs and trees as images.
* [GNUPlot](http://www.gnuplot.info/): Plotting tools used for assignments which display graphs and charts as images.
* [GDB](http://www.gnu.org/software/gdb/): The GNU Debugger. We do not officially offer a tutorial for this tool as Valgrind usually suffices, but GDB allows you to step through your code and test specific execution paths.
* [Subversion](http://subversion.tigris.org/): The revision control system used for turning in assignments. On systems which have a separate package (something like libsvn-dev or subversion-dev) for the header files, you’ll need those too.

After installing the required packages, you should now be able to check out, build, and run assignments as described in their documentation.

### Ubuntu >= 14.04
This should get you all of the packages you’ll need:
```
sudo apt-get update && sudo apt-get install clang-6.0 libc++abi-dev libc++-dev git gdb valgrind graphviz imagemagick gnuplot cmake
sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-6.0 100
sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-6.0 100
sudo update-alternatives --install /usr/bin/llvm-symbolizer llvm-symbolizer /usr/bin/llvm-symbolizer-6.0 100
```
If you have a different version of clang installed, you might need to remove it first. Alternatively, if you don’t mind using a different version of clang, you can use the other version instead—just make sure to test your code on EWS. (You should do that anyway.)

### Arch
This should get you all of the packages you’ll need:
```
sudo pacman -Sy base-devel clang gdb valgrind graphviz imagemagick git gnuplot cmake
```
You will also need to install (libc++)[https://aur.archlinux.org/packages/libc%2B%2B/] and (libc++-abi)[https://aur.archlinux.org/packages/libc++abi] from the AUR.

The default ``clang`` package should work (it’s currently at 6.0), but make sure to test your code on EWS (which will be using clang 5.0). (You should do that anyway.)

## macOS
If you experience difficulties installing the software listed below, then please come speak with a TA during office hours, a lab section, or by posting on Piazza.

### Compiler, Git
**Disclaimer: Especially since the clang versions on EWS and the Mac environment will be different as well as the LLVM environments, please be sure to test your code on EWS as well to make sure it works in our grading environment.**

Run
$
```
xcode-select --install
```
to install the Xcode commandline tools. You should run that command even if you already have the commandline tools installed—running it sets up Apple’s version of clang to look for headers in the “regular” *nix places.

Next, we will install the (Homebrew Package Manager)[https://brew.sh/] for macOS using the following command.

$
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Next, we need to install imagemagick and graphviz with brew. Run
$
```
brew install ghostscript imagemagick graphviz cmake
```

### GDB and Valgrind
**Disclaimer: The course has not properly tested nor fully tested the following instructions. We do not officially support gdb or valgrind natively on macOS.**

We will now use the Homebrew package manager to install gdb. Keep in mind this works only on High Sierra and older versions of macOS (Mojave requires special instructions, which can be followed in this link. (Mojave GDB Instructions)[https://stackoverflow.com/questions/52529838/gdb-8-2-cant-recognized-executable-file-on-macos-mojave-10-14])

$
```
brew install gdb
```

Configure gdb to be a signed application permitted to debug process (gdb will not work without doing this).

1. Open the Keychain Access app (can be found in Applications/Utilities or can be searched for).
2. Click Certificate Assistant > Create a certificate.
3. Set the name of the certificate to ``gdbcert``, ``Identity Type`` to ``Self Signed Root``, and ``Certificate Type`` to ``Code Signing``.
4. Check ``Let me override defaults`` and click ``Continue``.
5. Set ``Security Number`` to 1 and ``Validity Period`` to 1825 (this means you can use gdb with this certificate for 1825 days. Increase the number for more days. The max is 20 years). Click ``Continue`` again.
6. Keep clicking ``Continue`` till you see the screen named ``Key Pair Information``. For algorithm, select ``ECC`` and for ``Key Size`` select ``384 bits``.
7. Keep clicking ``Continue`` till you see the screen named ``Specify a Location For The Certificate``. For ``Keychain``, select ``System``.
8. Finally, you can click the ``Create`` button. You may be prompted for you computer password.
9. In the Keychain Access application, choose the ``System`` keychain on the left sidebar. Select ``gdbcert``. Right click and open the context menu. Select ``Get Info``. Exapnd the ``Trust`` section. Set the ``Code Signing`` property to ``Always Trust.
10. Quit the Keychain Access application.

Now, we will sign gdb. To do so, we must first kill the ``taskgated`` process using the following command.
$
```
sudo pkill taskgated
```
We must first wait for the ``taskgated`` process to restart. To check whether it has restarted, run the following and see if a ``/usr/libexec/taskgated`` entry pops up. (This can take up to one to two minutes).
$
```
sudo lsof | grep taskgated
```

Now, lets sign our gdb application. To do so, run
$
```
codesign -s gdbcert /usr/local/bin/gdb
```
where you may then be prompted for your computer’s username and password. You should now be able to use gdb to debug your code.

Next, we will need to use brew to install valgrind. (Valgrind is not supported on macOS Mojave yet)

To do so, run
$
```
brew edit valgrind
```
and change the URL in the ``head`` section from ``https://sourceware.org/git/valgrind.git`` to ``git://sourceware.org/git/valgrind.git`` then run the following
$
```
brew update
brew install --HEAD valgrind
<div class="alert alert-warning" role="alert" markdown="1"><i class="fa fa-exclamation-circle"></i> 
```
