# Network Configuration Behaviour Evaluation
<p>
	<img src="https://img.shields.io/badge/state-in progress-yellow" alt="alternatetext">
	<img src="https://img.shields.io/badge/version-1.0%20-blue" alt="alternatetext">
  <img src="https://img.shields.io/badge/language-Python 3-blue" alt="alternatetext">
</p>
Application of Graph Neural Networks (GNN) to evaluate the behavior of networks with different topologies and configurations.

## Overview 
Network modeling is essential to build optimization tools for networking. For instance, an accurate network model enables to predict the resulting performance (e.g., delay, jitter, loss) and helps to find the configuration that maximizes the network performance according to a target policy (e.g., minimize the end-to-end delay). 

Nowadays, network models are either based on packet-level simulators or analytical models (e.g., queuing theory). The former are very costly computationally, while the latter are fast but not accurate. In this context, Machine Learning (ML) arises as a promising solution to build accurate network models able to operate in real time. 

Recently, Graph Neural Networks (GNN) have shown a strong potential to be integrated into commercial products for network control and management. Early works using GNN have demonstrated an unprecedented capability to learn from different network characteristics that are fundamentally represented as graphs, such as the topology, the routing configuration, or the traffic that flows along a series of nodes in the network. In contrast to previous ML-based solutions, GNN enables to produce accurate predictions even in networks unseen during the training phase. Nowadays, GNN is a hot topic in the ML field and, as such, we are witnessing significant efforts to leverage its potential in many different fields (e.g., chemistry, physics, social networks). In the networking field, the application of GNN is gaining increasing attention and, as it becomes more mature, is expected to have a major impact in the networking industry.

## Problem Statement 
The goal of this challenge is to create a solution based on neural networks that estimates performance metrics given a network snapshot. More in detail, this solution (Fig. 1) must predict the resulting per-source-destination mean per-packet delay given: 
<ul>
<li>a network topology,</li>
<li>a network configuration (routing, queue scheduling)</li>
<li>a source-destination traffic matrix.</li>
</ul>
<div style="text-align:center"><img style="text-align:center" src="https://bnn.upc.edu/wp-content/uploads/2020/11/model_solution.png"></img></div>
<div><i>Figure 1: Schematic representation of the neural network-based solution requested</i></div>

## Baseline

As a baseline, we provide RouteNet [1], a Graph Neural Network (GNN) architecture recently proposed to estimate per-source-destination performance metrics (e.g., delay, jitter, loss) in networks. Thanks to its GNN architecture, RouteNet revealed an unprecedented ability to make acccurate performance predictions even in network scenarios unseen during the training phase, including other network topologies, routing configurations, and traffic matrices (Fig. 2).

<img src="https://i.ibb.co/XW1wBWX/Screenshot-2021-06-20-at-14-43-18.png"></img>
<div><i>Figure 2: Schematic representation of RouteNet</i></div>
<br><br>
In this challenge, we extend the problem to modeling network performance in the presence of different queue scheduling policies at network nodes. So far, RouteNet does not include support for modeling the impact of multi-queue scheduling policies on network performance and, consequently, it produces poor estimates of network scenarios that include such policies.

## Dataset

For this challenge, we provide a dataset generated with the OMNet++ network simulator, which is a discrete event packet-level network simulator. The dataset contains samples simulated in several topologies and includes hundreds of network configurations (routing, queue scheduling) and traffic matrices. Each sample is labeled with per-flow performance measurements (mean per-packet delay, jitter and loss) resulting from the simulation. In particular, this challenge focuses only on the prediction of mean per-packet delay for each flow.

In this challenge, we extend the problem to modeling network performance in the presence of different queue scheduling policies at network nodes. So far, RouteNet does not include support for modeling the impact of multi-queue scheduling policies on network performance and, consequently, it produces poor estimates of network scenarios that include such policies. We provide an open source implementation of RouteNet including a tutorial on how to use and modify fundamental characteristics of the model. Participants are encouraged to update RouteNet or submit their own neural network architecture.

Three different datasets will be provided for this challenge: 
<ul>
<li>training</li>
<li>validation</li>
<li>test</li>
</ul>

The training and validation datasets include the per-flow performance measurements (output labels). These datasets will be released at the beginning of the challenge. The test dataset will not include any per-flow performance measurements, and it will be used at the evaluation phase to test the accuracy of the proposed solutions. See tentative release dates at the “Timeline” section.

The training dataset contains samples simulated in two different network topologies, while the validation and test datasets include samples simulated in a different topology.

## Evaluation
Before the end of the challenge, we will provide a test dataset. This dataset will contain samples with similar distribution to the samples present in the validation dataset. Participants must label this dataset with their neural network models and send the results in CSV format. For the evaluation, we will use the Mean Absolute Percentage Error (MAPE) score computed over all the source-destination delay predictions produced by the candidate solutions:

<img src="https://bnn.upc.edu/wp-content/uploads/2020/11/evaluation.png"></img>

Solutions with lower MAPE score will be the winners.

<b>Note:</b> The test datset will not include any data of performance measurements (i.e., per-flow delay, jitter and loss). It means that any of these features can be used as input of the proposed solutions. For those using the dataset API, they can assume that NO data under the performance_matrix data structure can be used as input for the model.

## Resources

<ul>
<li><b>Training/validation datasets</b> (https://challenge.bnn.upc.edu/dataset)</li>
<li><b>API</b> to easily read data from the datasets provided (https://github.com/knowledgedefinednetworking/datanetAPI/tree/challenge2020 )</li>
<li><b>Baseline:</b> RouteNet implementation in TensorFlow 2.1 including a brief tutorial (https://github.com/knowledgedefinednetworking/RouteNet-challenge)</li>
</ul>

## Author

- Mario Sessa (@kode-git)

## License

&copy; Apache License Version 2.0, January 2004
