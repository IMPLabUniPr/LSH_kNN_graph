# LSH_kNN_graph
[[paper](https://arxiv.org/)] [[project](http://implab.ce.unipr.it/?page_id=)] 

The proposed method allows to create an approximate kNN graph in C++ for the diffusion application.
Then the retrieval is tested and the performance are the same or better than the ones obtained on the brute-force graph, but in less time (due to the reduction in the approximate kNN graph creation).


## Datasets
The original dataset files are converted in binary through the application of a simple C++ script:
- [Oxford5k](https://drive.google.com/)
- [Oxford105k](https://drive.google.com/) 

After downloading the dat files you need to create a folder called `dataset ` and then put in the uncompressed version.

## Installation
* Requirements:
  * G++ 5.4 or greater
  * openmp
  * cblas  
* Build:
` g++ -o LSH_sparse LSH_sparse.cpp -lstdc++fs -std=c++14 -fopenmp -O2 -lcblas`

## Test

LSH kNN (δ = 6, L = 20, th = 5000):
`./LSH_sparse 6 20 oxford5k false 5000 0 ResNet50`

multi LSH kNN graph (δ = 6, L = 20, th = 5000, 80% of multi-probe LSH):
`./LSH_sparse 6 20 oxford5k false 5000 80 ResNet50`


## Results

### Oxford5k
 
 In every test, the neighborhood is setted to 1.

| Configuration        | LSH projection           | kNN graph creation | mAP |
| :------------- |:-------------:| :-----:| :---:|
| LSH kNN graph (δ = 6, L = 20) | 0.45 s   | 0.52 s | 90.97% |
| LSH kNN graph (δ = 8, L = 10) | 0.4 s   | 0.94 s | 88.98% | 
| multi LSH kNN graph (δ = 6, L = 2) | 0.29 s   | 1.54 s   | 91.13%   | 
| NN-descent (1) | -   | 55 s   | 83.81%   | 
| RP-div (2) | -   | 1.16 s   | 82.68%   | 
| brute-force | -   | 1.33 s   | 90.79%   | 


### Oxford105k

| Configuration        | LSH projection           | kNN graph creation | mAP |
| :------------- |:-------------:| :-----:| :---:|
| LSH kNN graph (δ = 6, L = 20) | 23 s   | 77 s | 92.50% |
| LSH kNN graph (δ = 8, L = 10) | 15 s   | 145 s | 90.79% | 
| multi LSH kNN graph (δ = 6, L = 4) | 5s   | 420 s   | 92.85%   | 
| brute-force | -   | 4733 s   | 91.45%   | 



## Reference

<pre>@article{magliani2018efficient,
  title={Efficient Nearest Neighbors Search for Large-Scale Landmark Recognition},
  author={Magliani, Federico and Fontanini, Tomaso and Prati, Andrea},
  journal={arXiv preprint arXiv:1806.05946},
  year={2018}
}

@inproceedings{dong2011efficient,
  title={Efficient k-nearest neighbor graph construction for generic similarity measures},
  author={Dong, Wei and Moses, Charikar and Li, Kai},
  booktitle={Proceedings of the 20th International Conference on World Wide Web},
  pages={577--586},
  year={2011},
  organization={ACM}
}

@inproceedings{sieranoja2018fast,
  title={Fast random pair divisive construction of kNN graph using generic distance measures},
  author={Sieranoja, Sami and Fr{\"a}nti, Pasi},
  booktitle={Proceedings of the 2018 International Conference on Big Data and Computing},
  pages={95--98},
  year={2018},
  organization={ACM}
}

</pre>
