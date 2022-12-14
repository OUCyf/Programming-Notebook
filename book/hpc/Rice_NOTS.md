# NOTS

- Author: *{{Fu}}*
- Update: *Dec 15, 2022*
- Reading: *10 min*

---


## Apply an Account

Set up on the cluster (NOTS) please follow the instructions to apply for an account, https://kb.rice.edu/108221, and put your advisor down as
your sponsor if your PI has the account.

```{figure} ./files/nots-account.jpg
---
scale: 30%
align: center
name: nots-account
---
NOTS Account Application
```


## File Management

The following is my data managerment, more info please refer to [Rice CRC Tutorial](https://kb.rice.edu/108237).



```{figure} ./files/nots-storage.jpg
---
scale: 30%
align: center
name: nots-storage
---
NOTS Storage 
```


:::{warning}
- `/scratch` is not permanent storage, which is to be used only for job I/O.  Delete everything you do not need for another run at the end of the job or move to `/storage/hpc/work` for analysis. Staff may periodically delete files from the `/scratch` file system even if files are less than 14 days old.

- `/storage/hpc/work` is only available on the login nodes. Data can be copied between `/storage/hpc/work` and `/scratch` before/after running jobs.
:::


## Computing Resources

```{figure} ./files/cpu_gpu.jpg
---
scale: 50%
align: center
name: cpu_gpu
---
NOTS Resources 
```

## Teriminal Configuraion

NOTS is a `Red Hat` linux system, the default shell is `bash`.
Becasue I'm not the administrator, so I don't have the root permissions,
which means I can't use `yum` to install packages. 


In addition, I can't change the default shell from `bash` to `zsh` by myself, 
but I let the administrator change it to `zsh` which is a old version.
So I install `zsh` by myself, and auto-run new zsh when I login.


```bash
# use wget to download source package 
wget -O zsh.tar.xz https://sourceforge.net/projects/zsh/files/latest/download

# decompress the package
xz -d zsh.tar.xz
tar -xvf zsh.tar

# configuration
cd zsh
./configure --prefix=/storage/hpc/work/ja62/fy21/software/zsh/bin/zsh

# install
make 
make install

# auto launch when login bash
vim ~/.bashrc
export PATH=/storage/hpc/work/ja62/fy21/software/zsh/bin:$PATH
```


:::{admonition} How to start new `zsh` when login?
:class:  dropdown
```bash
vim ~/.zshrc

# Output:
# [1].run Fu's zsh when login at the first time
ZshName=$(which zsh)
if [ "$ZshName" = "/usr/bin/zsh" ];then
  export PATH=/storage/hpc/work/ja62/fy21/software/zsh/bin:$PATH
  echo "Now run Fu's zsh...\nVersion: $(zsh --version)\nPath: $(which zsh)\n"
  zsh
fi
export PATH=/storage/hpc/work/ja62/fy21/software/zsh/bin:$PATH


# [2].source global definitions
if [ -f /etc/zshrc ]; then
	. /etc/zshrc
fi
```
::::


**Some packages I have installed:**

|        Name       |       Purpose       |        Url        |         Date        |
|    ------------   |    -------------    |  :-------------:  |   :-------------:   |
|     `miniconda`   |                     |                   |                     |
|     ``            |                     |                   |                     |
|     ``            |                     |                   |                     |




**Conda list:**

**scientific computation-related package**:

|    Name       |    Purpose    |    Way       |     
| ------------  | ------------- | :----------: |
| `numpy`       | ...           | conda  |
| `matplotlib`  | ...           | conda  |
|  ``   |   |
|  ``   |   |



## Job Example

The following is an example named with `jobs.slurm`,
and some common command to run the job.


```bash
# submit a job
sbatch jobs.slurm

# check the state of job
sacct -j JobID
```

**The `jobs.slurm` content:**

```bash
#!/bin/bash 
##################################### 
# Mission name
#SBATCH --job-name=fy-test

# Use only single node 
#SBATCH -N 1 

# SMP execution, only one task 
#SBATCH -n 1 

# Use physical cores only not hyperthreads 
#SBATCH --threads-per-core=1 

# Request multiple cores 
#SBATCH --cpus-per-task=1 

# Time for your request 
#SBATCH --time=00:10:10


#SBATCH --gres=gpu:1 


# load package
module load GCC

# run job
srun echo "ssss" >> 2.txt
srun python ./mission.py

```

:::{warning}
Note there is no blank space between `#` and `SBATCH`, otherwise it will get an error.
For example:

```bash
# Use only single node 
#SBATCH -N 1 
```
:::

