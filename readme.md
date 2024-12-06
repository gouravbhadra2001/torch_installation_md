**Date Created:** Friday, August 17, 2024

# hi folks! How are you

# **Author: GOURAV**  

**PLEASE FOLLOW THE FOLLOWING GUIDE TO INSTALL PYTORCH FOR GPU IN VIRTUAL ENVIRONMENT AND DO THE PROJECT**

## Important Links

Here are some important links related to this project:

- [Official PyTorch Documentation](https://pytorch.org/docs/stable/index.html)
- [PyTorch Installation Guide](https://pytorch.org/get-started/locally/)
- [NVIDIA CUDA TOOLKIT All Versions](https://developer.nvidia.com/cuda-toolkit-archive)
- [NVIDIA Driver Download](https://www.nvidia.com/Download/index.aspx)
- [Python Official Website](https://www.python.org/)

---

# VERSION SPECIAL

**Python 3.10.12**  
**Ubuntu 22.04**  
**Pytorch with CUDA 12.1**  
**NVIDIA DRIVER NAME: nvidia-driver-535 (proprietary, tested)** [No "open", no "server"]  
**If you have everything's version exactly the same as me, after virtual environment setup, you can perform required python package installation simply by running the command in terminal:**

```bash
pip install -r requirements_classify.txt
```

## PROCESS OF INSTALLATION WITH GPU SETUP

**Step 1:**  
In Ubuntu: Show Applications > App: Software & Updates > Tab: Additional Drivers > Radio Button: Using NVIDIA-driver metapackage from nvidia-driver-535 (proprietary, tested) > Apply Changes > (Now wait until the changes are applied) > Restart PC

**Step 2:**  
Using the previous step, only check that the change is applied or not, if applied then close.

**Step 3:**  
In terminal (`Ctrl` + `Alt` + `T`), test the command:

```bash
nvidia-smi
```

- Check the status of your NVIDIA GPU is shown or not.
- If the status is shown, note that in the top-left, your NVIDIA-SMI version, top-middle NVIDIA Driver Version, somewhere left GPU name and in the top-right the version of CUDA the current driver uses are shown. You can see the recent GPU memory and fan utilization records and many more.  
- In my case:
  - GPU name: NVIDIA Geforce GTX 1650
  - NVIDIA-SMI version: 535.183.01
  - NVIDIA Driver version: 535.183.01
  - CUDA version: 12.2

**Step 4:**  
Now set up a virtual environment in Python. Here's how you can do:

1. First check whether python is installed or not. In my case, during installation of Ubuntu 22.04, python3 with the specified version has been automatically installed without pip. If your Ubuntu does not automatically do, you can check by running command:

   ```bash
   python3
   ```

   If not installed, please follow online documentation for installing python of specified version specifically.

2. First check whether pip3 is installed or not:

   ```bash
   pip3 --version
   ```

3. If not installed:

   ```bash
   sudo apt install python3-pip
   ```

4. Now run:

   ```bash
   pip3 freeze
   ```

   or:

   ```bash
   pip freeze
   ```

   to check the packages installed. You can find many Python packages installed, but we're not gonna work with them now.

5. Now think the environment name of Python. The name is actually of a folder of environment. Let's say, "ml".

6. Probably you don't have the virtual environment installed. So install it by running:

   ```bash
   sudo apt install python3.10-venv
   ```

7. Now run:

   ```bash
   python3 -m venv ml
   ```

   Your environment is created but not activated. Now you can find a folder named "ml" in your current directory. The folder "ml" contains folders `bin`, `include`, `lib`, `lib64`, `share` and a file named `pyvenv.cfg`. Whatever packages you will install using pip will be located in `ml/lib/python3.10/site-packages`.

8. Now look, within the `ml` folder, the `bin` folder contains many files including a plain text file named `activate`. We have to use this file to activate the environment named "ml". How to do this? Follow-up:

   - In which directory you were there during the installation of all instructed so far, stay there, don't leave. Check whether you can find the `ml` folder after running command:

     ```bash
     ls
     ```

   - If yes, you can find it out, then just remember the path of the `activate` file: `ml/bin/activate`, so to use this, just use the command:

     ```bash
     source ml/bin/activate
     ```

9. Runned? Wow. Now check, the current line of the terminal your cursor blinking in, is prefixed with "(ml)" and whatever command you run onwards in next lines, all these lines will be prefixed with this same. What does it mean? Yeah, your environment is activated. Now whatever package you will install from now, will be saved to `ml/lib/python3.10/site-packages` and in this same folder path, the packages or libraries you will import in your Python code while being under this ml environment, will be accessed by the program to search for the called packages or the libraries.

   Let me clarify with an example. Suppose, you have installed a Python package using pip before activating the ml environment. Say, this package is "flask". This time, as you have not activated ml environment, you are using your default environment and whatever you install in Python this time, all are saved in the site-packages folder of the Python3.10 in your root directory of Ubuntu. This time, if you write a Python code that includes `import flask`, you won't get an error, as the root directory's Python3.10 folder is accessed by the program. But once you run this program while the ml environment is activated, you will surely get the "no module named 'flask'" error as you have not installed the flask within this environment and from your current directory, the program is accessing the path `ml/lib/python3.10/site-packages`, where no such file named `flask.py` is there at all. This is the importance of the environment.

10. Now, if you have not installed anything after the activation of ml, you will not get any output after running:

    ```bash
    pip3 freeze
    ```

    or:

    ```bash
    pip freeze
    ```

    command which is used to show which packages have been installed so far.

11. So, before installing anything, perform the best practice. First create a separate folder within the current directory for your project you will do now, say folder name: "imageClassification". Now enter into the folder by running:

    ```bash
    cd imageClassification
    ```

    Now within this, create a txt file, any name you can prefer for it. Say, "cheats.txt". So, to create it, run:

    ```bash
    touch cheats.txt
    ```

    This will create the `cheats.txt` file only, with empty content. Now test one thing. Run:

    ```bash
    pip install numpy
    ```

    This will install numpy in ml env. If you run:

    ```bash
    pip freeze
    ```

    you can see only the numpy package name with its latest version number, compatible with your current env version. Now open the `cheats.txt` file from your file system, you can see it is empty, close it. Run the command:

    ```bash
    pip freeze > cheats.txt
    ```

    Now open again `cheats.txt`. Wow, that contains the numpy package name with its version!! Amazing, isn't it? Now whenever you install anything using pip in the current environment and update the `cheats.txt` with the command:

    ```bash
    pip freeze > cheats.txt
    ```

    then this will contain the names and versions of all the packages installed so far. Now why to do that? Suppose you share your friend this `cheats.txt`, he/she saves it in his/her current directory and with the same version of Python and all other basic dependencies installed and active, your friend need not to memorize which packages you have installed, he/she just runs:

    ```bash
    pip install -r cheats.txt
    ```

    and all the same packages with the specified versions will be installed in his/her current environment. And if you share your project files with him/her easily your project codes will run on his/her device without any error. You can use this technique for running the same project in a cloud or on your other devices also.

12. Now do one thing, each time you install a new package for the project, never forget to update this `cheats.txt`.

13. If you wanna uninstall all the packages, simply run:

    ```bash
    pip uninstall -r cheats.txt
    ```

14. If you wanna deactivate the current environment, I mean for simply getting out of this env, just run:

    ```bash
    deactivate
    ```

    and notice the change. For now, there are more processes onwards, so don't leave the env, stay there.

**Step 5:**  
Wow, congrats, you have successfully created the environment. If you have not uninstalled numpy, do it, because, right now it is of no use. Just brush up, you have already the NVIDIA driver there, you need not to install any CUDA toolkit manually from CUDA's official website's download releases, PyTorch is already there for you.

**Step 6:**  
Go to the official website of PyTorch: [https://pytorch.org](https://pytorch.org). Scroll a little and you can find the "INSTALL PYTORCH" section. If not, then scroll up completely and click on the call-to-action button "Get Started >", you will be redirected to "Start Locally Section", which contains the installation guide. Or from the browser, you can also use the URL: [

<https://pytorch.org/get-started/locally/>](<https://pytorch.org/get-started/locally/>). By default, the Start Locally tab is active.

**Step 7:**  
Make sure the following are selected (The version numbers are of the time, I am writing this readme, in your time, these may be different):

- PyTorch Build: Stable (2.4.0)
- Your OS: Linux
- Package: Pip
- Language: Python
- CUDA: 12.1

Note that, depending on the CUDA version selected, the pip installation commands in "Run this Command" changes. In my case, you know the CUDA, my driver uses is of version 12.2, so I better opt for either 12.1 or 12.4, [I had the options 11.8, 12.1, 12.4] because:

1. There is no 12.2 in this PyTorch installation guide
2. The small command for 12.1 seems to install default safe settings
3. There remain always frustrating bugs in recent versions, here it is 12.4.

Here are the commands in my time:

- For 11.8:

  ```bash
  pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
  ```

- For 12.1:

  ```bash
  pip3 install torch torchvision torchaudio
  ```

- For 12.4:

  ```bash
  pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124
  ```

- For ROCm 6.1:

  ```bash
  pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm6.1
  ```

- For CPU:

  ```bash
  pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
  ```

I chose the second one. Now your decision comparing with my situation, which command you will copy. Please don't copy the PyTorch installation command from this README guide. Copy what your time's PyTorch website is showing you, just like I followed.

**Step 8:**  
So copied! Now, in the terminal, I hope you have not left the env. Now paste this installation command in the terminal and run. Depending on your network and the hardware you're using, the installation will take time. So, keep patience, meditate, sing or scroll reels, what suits for you to pass the time of waiting.

**Step 9:**  
Installation over? Good, now just test the Python code in the current environment:

```python
import torch
print(torch.cuda.is_available())  # If PyTorch is using your dedicated GPU, this should be True
print(torch.cuda.get_device_name())  # If PyTorch is using GPU, the GPU name should be displayed. In my case, this is NVIDIA GeForce GTX 1650
```

**Step 10:**  
Congratulations! You have set up PyTorch with your GPU. Now if you wanna do this project, install some more things:

```bash
pip3 install scikit-learn h5py numpy pillow seaborn matplotlib
```

And after installation run:

```bash
pip freeze > cheats.txt
```

**Step 11:**  
Now, by default, there was no live GPU performance visualization in my Ubuntu. As in Windows Task Manager, if the same in your case, then install `nvtop` running the command:

```bash
sudo apt install nvtop
```

And then run:

```bash
nvtop
```

You will be amazed with the live visualization within the terminal with live GPU usage changes and graphs if you are training PyTorch model or gaming/editing video over GPU - in the first case, see the changes in "compute" and in the second case, "graphics". Another way, you can monitor the GPU utilization, by running:

```bash
watch -n0.1 "nvidia-settings -q GPUUtilization -q useddedicatedgpumemory"
```

But this will just give the written changes only, not the amazing visualization of `nvtop`.

**Step 12:**  
Now do whatever you wanna do with the project you cloned.

---

**Hope all these cleared many things related to installation process. One more time, I am saying, always give the most importance to the versions of any package, environment, OS or programming language you use in order to avoid any kind of frustrating dependency issue.**

**In any case, it is recommended to follow official documents and popular forums like Stack Overflow, Reddit etc.**

---

## Important Links

Here are some important links related to this project:

- [Official PyTorch Documentation](https://pytorch.org/docs/stable/index.html)
- [PyTorch Installation Guide](https://pytorch.org/get-started/locally/)
- [NVIDIA CUDA TOOLKIT All Versions(https://developer.nvidia.com/cuda-toolkit-archive)]
- [NVIDIA Driver Download](https://www.nvidia.com/Download/index.aspx)
- [Python Official Website](https://www.python.org/)

**Date Created:** August 17, 2024

---
