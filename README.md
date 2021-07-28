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
