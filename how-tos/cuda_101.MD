## CUDA
Short description on CUDA programming

* __global__ keyword: indicates that the following function will run on the GPU, and can be invoked globally, which in this context means either by the CPU, or, by the GPU. Functions defined with the __global__ keyword return void type.
* Host code: is referred to code executed on the CPU.
* Device code: is referred to code executed on the GPU.
* Nvcc: nvidia cuda compiler.
``` bash
# Example of one cuda compiler call
!nvcc -arch=sm_70 -o hello-gpu 01-hello/01-hello-gpu.cu -run
```
* Grid configuration: consists of number of blocks and number of threads per block.
* Kernel: GPU function that has grid configuration on launch and is run in paralel on every thread in grid.
* Variables available inside every kernel:
``` c++
threadIdx.x; // Variable that states id of current thread in one kernel's block
blockDim.x;  // Variable that states number of threads per block
blockIdx.x;  // Variable that states id of block in which is thread that is executing current code
gridDim.x;   // Variable that states number of kernel's blocks
```
* Maximum thread number per block: 1024
* Optimal blocks number: should be multiple of 32, due to GPU hardware traits.
* Grid-Stride Loops: if number of elements in array is greater then number of threads, thread must process more then one element:
``` c++
__global__ void kernel(int *a, int N)
{
  int index_within_the_grid = threadIdx.x + blockIdx.x * blockDim.x;
  int grid_stride = gridDim.x * blockDim.x;

  for (int i = index_within_the_grid; i < N; i += grid_stride)
  {
    // Do work on a[i];
  }
}
```
* Error handling macros:
``` c++
// Error macro
inline cudaError_t checkCuda(cudaError_t result)
{
  if (result != cudaSuccess) 
  {
    fprintf(stderr, "CUDA Runtime Error: %s\n", cudaGetErrorString(result));
    assert(result == cudaSuccess);
  }
  return result;
}

// check async errors
checkCuda(cudaGetLastError());
//check sync errors
checkCuda(cudaDeviceSynchronize());
```
* Grid dimensions: can be 2d and 3d for accelerating matrixes and other 3d structures.
``` c++
dim3 threads_per_block(16, 16, 1);
dim3 number_of_blocks(16, 16, 1);
someKernel<<<number_of_blocks, threads_per_block>>>();
```
* Nsys: nsight Systems command line tool, is a powerful tool for profiling accelerated applications
``` bash
nsys profile --stats=true
# --stats=true -> get summary
# -f -> overwrite previous report
```
* Streaming Multiprocessors (SMs): blocks of threads are run on SMs, depending on number of SMs and requirements of a block, more then one block can be scheduled on an SM.
* Performance gains: 1. By choosing a grid size that has a number of blocks that is a multiple of the number of SMs on a given GPU
		      2. SMs execute groupings of 32 threads from within a block that are called warps. That is why choosing thread number as multiple of 32 can give performance boost.
* Get information: about currently used nvidia GPU where code is executed:
``` c++
int deviceId;
int numberOfSMs;
cudaGetDevice(&deviceId);                  // deviceId: now points to the id of the currently active GPU.

//cudaDeviceProp props;
//cudaGetDeviceProperties(&props, deviceId); // props: now has many useful properties about the active GPU device. (etc number if SMs)

cudaDeviceGetAttribute(&numberOfSMs, cudaDevAttrMultiProcessorCount, deviceId);
int numberOfBlocks = 32 * numberOfSMs;
int numberOfThreads = 32 * 8; // 256 
```
* Unified Memory: When Unified Memory is allocated, the memory is not resident yet on either the host or the device. When either the host or device attempts to access the memory, a page fault will occur, at which point the host or device will migrate the needed data in batches.  Similarly, at any point when the CPU, or any GPU in the accelerated system, attempts to access memory not yet resident on it, page faults will occur and trigger its migration.
* Asynchronous Memory prefetching: prefetch memory that will be later used on specific device. 
``` c++
int deviceId;
// The ID of the currently active GPU device.
cudaGetDevice(&deviceId);

// Prefetch to GPU device.
cudaMemPrefetchAsync(pointerToSomeUMData, size, deviceId);
// Prefetch to CPU device. cudaCpuDeviceId is built in cuda variable
cudaMemPrefetchAsync(pointerToSomeUMData, size, cudaCpuDeviceId);
```
* Stream: series of commands that execute in order. There are two types of streams default stream and non-default created streams.
* Stream rules: 
                1. Operations within a given stream occur in order.
                2. Operations in different non-default streams are not guaranteed to operate in any specific order relative to each other.
                3. The default stream is blocking and will both wait for all other streams to complete before running, and, will block other streams from running until it completes.
* Cuda stream is forth argument: (3rd argument of the execution configuration allows programmers to supply the number of bytes in shared memory to be dynamically allocated per block for this kernel launch, default is 0):
``` c++
cudaStream_t stream;       // CUDA streams are of type cudaStream_t
cudaStreamCreate(&stream); // Note that a pointer must be passed to cudaCreateStream

someKernel<<<number_of_blocks, threads_per_block, 0, stream>>>(); // Stream is passed as 4th EC argument

cudaStreamDestroy(stream); // Note that a value, not a pointer, is passed to cudaDestroyStream
```
Nsight Systems: application for visually profiling the timeline of GPU-accelerated CUDA applications.
