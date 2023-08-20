# Entropy-Aware I/O Pipelining for Large-Scale Deep Learning on HPC Systems

## Motivation

​	In order for I/O support keep up with the growth of computing power for deep neural networks.

​	Need  a specialized, high-performance I/O solution that can construct highly-randomized large minibatches for the DNN training

## Aim

​	coordinate the use of memory, communication, and I/O resources for efﬁcient training

## Main Idea

​	1.An I/O framework,Deep IO, for DNN

​		1.1.RDMA-assisted in-situ shuffing

​		The storage buffer is used to store the dataset in memory, the read buffer is used the destination of dataset shuffling. The suffle operation occurs in-situ with the placement of the elements into the read buffer.

​		1.2.Input pipelining

​		To overlap disk I/O when the storage buffer is not able the entire dataset.

​			The entire dataset resides in memory--In-memory pipeline: move elements from local and remote storage buffers in a pipeline manner,overlapping training with mini-batch preparation.

​			The datasets cannot be fully uploaded to the storage buffers--Hybrid backend-memory pipelin(to reduce the overhead of constructing mini-batch): To allow the uploading time to be overlapped with training time, the read buffer divided into two equal-sized buffers.

​		1.3.Entropy-aware opportunistic ordering

​		In some trainiing job, the order of input is not important as long as the input order randomized. thus introduce entropy-aware opportunistic ordering.

​		The algorithm for determining the elements for mini-batches in opportunistic ordering is designed to avoid excessive inter-process communication using a seed broad-casting method, avoids a large number of small random reads from backend storage by utilizing only the elements that are loaded into the in-memory storage buffers

​	2.A portable API for DeepIO



## Strength

​		It can remove the need for additional memory copies of the mini-batch elements.

​		DeepIO as a prototype for TensorFlow featuring novel optimization.

​		Inmproves the I/O bandwidth compared with BeeGFS and Octopus.

## Weakness

