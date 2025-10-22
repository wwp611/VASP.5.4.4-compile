### **VASP COMPILE**


**Example: Transopt\_vasp.5.4.4 (NSCC-TJ Supercomputer System)**
---



###### **① vasp.5.4.4 compile**



**First of all, download the vasp zip and upload to your Supercomputer system. This is my GitHub website where exit vasp.5.4.4.tar.gz(https://github.com/wwp611/VASP.5.4.4-compile)**



cd your/file/path/ 

tar -zxvf vasp.5.4.4.tar.gz

cd vasp.5.4.4/

module load mlip/2-icc19.0-openmpi				## here you can see the output Loading mlip/2-icc19.0-openmpi

&nbsp;												##									 Loading requirement: Intel\_compiler/19.0.4 MPI/openmpi/4.1.2-mpi-x-icc19.0 MKL/19.1.2

cp arch/makefile.include.linux\_intel makefile.include

vim makefile.include								## we should replace "FC = mpiifort FCL = mpiifort -mkl=sequential -lstdc++" with "**FC = mpif90 FCL = mpif90 -mkl=sequential -lstdc++"** 													##and change the "intelmpi" in BLACS = -lmkl\_blacs\_intelmpi\_lp64, now it is **lmkl\_blacs\_openmpi\_lp64**. And replace CC = icc CXX = icpc 													##with **CC = mpicc CXX = mpicxx**

make all											## take a tea break and wait for 20+ moments



Then you can see the vasp\_gam  vasp\_ncl  vasp\_std in fold bin/ , that is all.



###### **②vasp.5.4.4.vk and vasp.5.4.4.symm version compile**



###### **.VK version**



git clone https://github.com/yangjio4849/TransOpt.git

cp /fs2/home/lizhenwar/software/TransOpt/for\_vasp.5.4.4/main.F\_for\_vk main.F

cp /fs2/home/lizhenwar/software/TransOpt/for\_vasp.5.4.4/getnabij.F .

module purge

module load mlip/3-icc19.0-openmpi

cd src/

vi .objects							**## add getnabij.o after elphon.o \\ at the end of the SOURCE=\\ section. (ATTENTION ! ! !)**

make all



Then you can see the same result of vasp compile



###### **.SYMM version**



cd vasp.5.4.4.symm/

cd src/

cp /fs2/home/lizhenwar/software/TransOpt/for\_vasp.5.4.4/main.F\_for\_symm main.F

module purge

module load mlip/3-icc19.0-openmpi

make all



###### **③TransOpt compile**



**for the full version detail please read https://github.com/yangjio4849/TransOpt/**



git clone https://github.com/yangjio4849/TransOpt.git		

module purge

module load abinit/9.6.2-icc19.0-mpi-x

bash omprun



Then you can see derivation\* TransOpt\_2.0\* TransOpt\_omp\_2.0\*




