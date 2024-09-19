# Installation
### Install Python library
```shell
pip install expAscribe
```

### Virtualenv

If you encounter dependent version conflicts during the installation process.
You can try to create a virtual environment and install it.

```shell
pip install virtualenv
virtualenv <your_env>
source <your_env>/bin/activate # Linux/macOS
<your_env>\Scripts\activate  # Windows
pip install expAscribe
```

### Conda

Since the installation of this way requires conda, please install [Anaconda](https://www.anaconda.com/download) first.

```shell
conda create -n <your_env> python=3.10
conda activate <your_env>
pip install expAscribe
```

Here is a way in Linux to install Anaconda.

```shell
wget https://repo.anaconda.com/archive/Anaconda3-2023.10-Linux-x86_64.sh
bash Anaconda3-2023.10-Linux-x86_64.sh
source ~/.bashrc
export PATH="$HOME/anaconda3/bin:$PATH"
source ~/.bashrc
```
