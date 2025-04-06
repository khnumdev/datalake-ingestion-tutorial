# Datalake with lambda tutorial

## Contributing

We welcome contributions! Please see the [CONTRIBUTING.md](CONTRIBUTING.md) file for guidelines on how to contribute to this project.

## Introduction

### Prerequisites
Before diving into this tutorial, ensure you have the following:
- A valid [Azure account](https://azure.microsoft.com/free/).
- The [Azure CLI](https://learn.microsoft.com/cli/azure/install-azure-cli) installed and configured on your local machine. Run `az --version` to confirm installation.
- Basic knowledge of cloud services and IoT concepts.

### About the Raspberry Azure IoT Emulator
This tutorial utilizes the [Raspberry Azure IoT Emulator](https://azure-samples.github.io/raspberry-pi-web-simulator/), a powerful tool that simulates IoT devices and helps you test Azure IoT scenarios without the need for physical hardware. By using this emulator, you can:
- Simulate data streams from IoT devices.
- Test data ingestion into Azure services like IoT Hub, EventHub, and Storage Accounts.

### Data Lake Lambda Architecture Overview
The Lambda architecture is a design pattern that combines batch and stream processing for handling large-scale data efficiently. It consists of three layers:
1. **Batch Layer**: Stores all the data and precomputes batch views for analysis.
2. **Speed Layer**: Handles real-time data processing for low-latency access.
3. **Serving Layer**: Merges batch and real-time results for querying.

In this tutorial, we'll implement a simplified version using Azure services to demonstrate key concepts. For a deeper dive into Lambda architecture, check out this [documentation]https://learn.microsoft.com/en-us/azure/architecture/databases/guide/big-data-architectures#lambda-architecture).

# Part 1: Data Lake with Lambda

## Step 1: Create an IoT Hub

To set up the IoT Hub, you'll use Azure CLI commands. Start by logging in to your Azure account using the `az login` command. This will prompt you to authenticate in your browser. If something is incorrect during any command execution, the Azure CLI will provide an error message detailing the issue.

Next, define environment variables to store important resource names that will be used throughout the tutorial:
```
RESOURCE_GROUP_NAME="MyResourceGroup"
IOT_HUB_NAME="MyIoTHub"
LOCATION="westeurope"
```

Export these variables to ensure they're accessible in subsequent commands:
```
export RESOURCE_GROUP_NAME
export IOT_HUB_NAME
export LOCATION
```

Create a resource group to organize your resources:
```
az group create --name $RESOURCE_GROUP_NAME --location $LOCATION
```

Set up the IoT Hub within this resource group:
````
az iot hub create --resource-group $RESOURCE_GROUP_NAME --name $IOT_HUB_NAME --location $LOCATION
```

Use unique and descriptive names for your resources, following [Azure's naming conventions](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/resource-name-rules) to ensure compatibility across services.


