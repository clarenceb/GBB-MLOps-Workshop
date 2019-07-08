# GBB MLOps Workshop

In this tutorial, you will learn how to train your own image classification model using [transfer learning](https://cs231n.github.io/transfer-learning/).

The Azure Machine Learning python SDK's [PyTorch estimator](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-train-pytorch) enables you to easily submit PyTorch training jobs for both single-node and distributed runs on Azure compute. The model is trained to classify dog breeds using a pretrained ResNet18 model that has been trained on the [Stanford Dog dataset](http://vision.stanford.edu/aditya86/ImageNetDogs/). This dataset has been built using images and annotation from ImageNet for the task of fine-grained image categorization. To reduce workshop time, we will use a subset of this dataset which includes 10 dog breeds.

## Prerequisites

* A laptop where you can install and run local applications
* [Azure Subscription](https://azure.microsoft.com/en-us/free/) with [Contributor](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#contributor) role or a pre-created [Resource Group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) where you have [Contributor](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#contributor) role assigned to your Azure AD user.
* Access to the Following Azure resources:
    - Azure Machine Learning Service
    - Azure Container Registry
    - Azure Storage Account
    - Azure Key Vault
    - Azure Application Insights
    - Azure Kubernetes Service
    - Azure Virtual Machines
* (Optional) Access to GPU VM SKUs (e.g. `Standard_NC6` or `Standard_NC6s_v2`) -- otherwise substitute for a CPU SKU; training may take longer.

Check that the Azure resources and [VM series](https://azure.microsoft.com/en-us/global-infrastructure/services/?products=virtual-machines) you will use are [available in your region](https://azure.microsoft.com/en-us/global-infrastructure/services/?products=); otehrwise choose a different region for these services.

## Training and test data

You can view the subset of the data used [here](breeds-10).

## Local environment setup

If you plan to use a local development environment, follow these steps.

### Install Miniconda

Install Miniconda for your OS (Windows/macOS/Linux): https://docs.conda.io/en/latest/miniconda.html

### Install Python dependencies

Follow these [Python SDK steps](https://docs.microsoft.com/en-us/azure/machine-learning/service/setup-create-workspace#sdk) to create an isolated Python environment with the azureml-sdk, jupyter notebook and other required dependencies.

### Launch Jupyter Notebook

Open a terminal and change to the root directory where you cloned this git repository.

Launch Jupyter Notebook:

```sh
jupyter notebook
```

## Workshop Guide

From the Jupyter notebooks interface, open the [dog-breed-classifier.ipynb](./dog-breed-classifier.ipynb) notebook and follow the instructions.

## Credits

* This workshop was forked from here: https://github.com/ronglums/PyCon-2019

## References

* [Azure Machine Learning Service docs](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml)
* [MLOps using Azure ML Services and Azure DevOps](https://github.com/microsoft/MLOpsPython)
* [Transfer Learning](https://cs231n.github.io/transfer-learning/)
* [The Jupyter Notebook](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html)
