# 19.10.06





# Once For All: Train One Network and Specialize it for Efficient Deployment



Progressive shrinking algorithm

​	prevent interference between many sub-networks

first train a neural network with maximum depth, width, and kernel size, then progressively train the network to support smaller sub-networks, preventing smaller sub-networks from hurting the accuracy of larger sub-networks. 

provide good initialization and better supervision for small sub-networks with the help of large
sub-networks rather than training them from scratch.

​	

OFA

​	decouple the model training stage & model specialization stage

​	1) model training stage

​		train a single OFA

​			subnetworks with different architectural configurations can be generated

​	2) model specialization process

​		prebuild the accuracy table and efficiency table for a subset of sub-networks

​	3) test stage

​		query the accuracy table and hardware latency table




