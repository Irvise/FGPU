# My best guess
all:
	xlC_r -O3 -qsmp=omp -qoffload -c saxpy.cc -o saxpy_omp45_c.o
	xlcuf -O3 -c saxpy.cuf -o saxpy_cuda_f.o
	nvcc -O3 -rdc=true -DNVCC -arch sm_60 --compiler-bindir xlC_r -c saxpy.cu -o saxpy_cuda_c.o
	xlC_r -O3 -qsmp=omp -c main.cc
	xlC_r -O3 -qoffload -qsmp=omp -qcuda -o test_kernels main.o saxpy_cuda_f.o saxpy_omp45_c.o saxpy_cuda_c.o -lxlf90_r -lxlcuf -lxlfmath

debug:
	xlC_r -O0 -g -qsmp=noopt -qoffload -c saxpy.cc -o saxpy_omp45_c.o
	xlcuf -O0 -g -c saxpy.cuf -o saxpy_cuda_f.o
	nvcc -O0 -g -rdc=true -DNVCC -arch sm_60 --compiler-bindir xlC_r -c saxpy.cu -o saxpy_cuda_c.o
	xlC_r -O0 -g -qsmp=noopt -c main.cc
	xlC_r -O0 -g -qoffload -qsmp=noopt -qcuda -o test_kernels main.o saxpy_cuda_f.o saxpy_omp45_c.o saxpy_cuda_c.o  -lxlf90_r -lxlcuf -lxlfmath

clean:
	rm -f *.o mixed_lang_xlcuf mixed_lang_nvcc
	rm -f *.mod
	rm -f test_kernels
