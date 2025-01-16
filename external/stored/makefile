# Paths to tools and libraries
nvcc = "C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v10.0/bin/nvcc.exe"
cudalib = "C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v10.0/lib/x64"
tensorflow = "C:/Users/pcarril/Anaconda3/envs/MeshDeformNet2/Lib/site-packages/tensorflow/include"
TF_LIB = "C:/Users/pcarril/Anaconda3/envs/MeshDeformNet2/Lib/site-packages/tensorflow"

# Target: DLL build
all: tf_nndistance.dll

# Rule for linking the final DLL
tf_nndistance.dll: tf_nndistance_g.cu.obj tf_nndistance.cpp
	cl /LD /Fe:tf_nndistance.dll tf_nndistance.cpp tf_nndistance_g.cu.obj ^
	-I"$(tensorflow)" ^
	-L"$(cudalib)" ^
	-L"$(TF_LIB)" ^
	-ltensorflow_framework -lcudart

# Rule for compiling the CUDA file
tf_nndistance_g.cu.obj: tf_nndistance_g.cu
	$(nvcc) -c tf_nndistance_g.cu -o tf_nndistance_g.cu.obj ^
	-I"C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v10.0/include" ^
	-I"$(tensorflow)" ^
	--std=c++11 ^
	--expt-relaxed-constexpr ^
	-gencode arch=compute_75,code=sm_75 ^
	--compiler-bindir="C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/VC/Tools/MSVC/14.16.27023/bin/Hostx64/x64" ^
	--compiler-options="/MD /O2 /nologo -DWIN32 -D_WINDOWS -DNOMINMAX" ^
	-DGOOGLE_CUDA=1 -D_FORCE_INLINES

# Clean up intermediate files
clean:
	del tf_nndistance.dll
	del *.obj
