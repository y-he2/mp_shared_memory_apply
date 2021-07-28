# mp_shared_memory_apply
## A proper way to do parallel apply without copying the data across the processes using Multiprocessing?

It has 3 very nice features:
* Can apply any pickable function. 
* Can use any numpy.ndarray tensor (which was the original intention but should be applicable to any indicable data structure). 
* The target data will not be copied across the processses (unless the data are returned in ur function). 
* No extra 3rd party libraries required (unless u need them in ur function obviously). 
* Switch between Multiprocess and Multiprocessing backend, to be able to use in Jupyter and console. 

And 3 annoying limitations:
* The function to be applied has to be pickable (it's a limitation in Multiprocessing, currently I see no way walkaround it). 
* The function definition has to be in a Python module file to be imported. 
* Multiprocessing cannot return any object larger than 2GB (it's a limitation or bug in Multiprocessing). 
  * See https://github.com/uqfoundation/pathos/issues/217

# Usage
1. Define ur pickable function as a Python module and store it in the same folder as the boilerplate. 
2. Call ```parallel_tensor_apply( func_module_name, data_tensor, index_set, max_processes = 99, \**kwargs )``` where:
 * _func_module_name_ is ur function module file. 
 * _data_tensor_ is the indicable data u want the function to apply on. 
 * _index_set_ is the set containing the indicies of how the function should be applied. The parallel backend will distribute the task according to this set. 
 * _\*\*kwargs_ will be passed further as keyword arguments to ur function, note that it has to be the same for indicies, so they are rather constant parameters than some "extra indicies". 
 * _max_processes_ is the number of processes u wanna use. 
3. The data will then be automatically copied to shared memory and the function will be applied to it in parallel. 
