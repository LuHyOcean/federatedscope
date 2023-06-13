<h1 align="center">
    <img src="https://ocean-1317261461.cos.ap-chengdu.myqcloud.com/img/secfed.png" width="250" alt="secfed-logo">
</h1>


![](https://img.shields.io/badge/language-python-blue.svg)
![](https://img.shields.io/badge/env-conda-brightgreen)

**SecFed**——**面向云边安全协作的联邦学习平台，以应对掉线节点干扰、梯度泄露攻击等安全挑战**。该平台利用协作学习实现模型性能提升，无需将数据集中到中央服务器，以保护数据隐私，

主要特性：
<img src="https://ocean-1317261461.cos.ap-chengdu.myqcloud.com/img/Cloud%20Protection1.png" style="zoom: 50%;" />
-   **基于联邦学习的隐私共享技术**：本作品提出了一种基于联邦学习的隐私共享技术，旨在通过协作学习来共同提升模型性能，同时避免将参与方的数据集中到中央服务器。这种技术使得在保护数据隐私的前提下能够进行全局模型的训练和优化。

- <img src="https://ocean-1317261461.cos.ap-chengdu.myqcloud.com/img/Network2.png" style="zoom:50%;" />  **面向掉线节点干扰的共享安全聚合**：为了解决联邦学习中掉线节点干扰的问题，本作品提出了一种共享安全聚合的解决方案。该方案利用加密技术和冗余节点，确保数据聚合的安全性和可靠性，从而提高了联邦学习结果的准确性和可信度。

- <img src="https://ocean-1317261461.cos.ap-chengdu.myqcloud.com/img/Key%20Digital3.png" style="zoom:50%;" />  **面向拜占庭敌手的局部模型安全评估**：采用BARFED算法保护联邦学习全局模型，防御数据中毒和模型中毒等攻击。BARFED算法通过引入随机化和验证机制，确保数据聚合的安全和可靠性，无需依赖特定数据分布或参与者行为假设。

- <img src="README.assets/Protection4.png" style="zoom:50%;" />  **面向推理攻击的梯度泄露防御策略**：为了防止梯度泄露攻击，本作品采用了面向推理攻击的梯度泄露防御策略。该策略利用**深度变分信息瓶颈技术**，避免模型参数的泄露，并通过传输模型参数信息来聚合模型，以防止梯度泄露攻击的发生。

## 代码结构
```
FederatedScope
├── federatedscope
│   ├── core           
│   |   ├── workers              # Behaviors of participants (i.e., server and clients)
│   |   ├── trainers             # Details of local training
│   |   ├── aggregators          # Details of federated aggregation
│   |   ├── configs              # Customizable configurations
│   |   ├── monitors             # The monitor module for logging and demonstrating  
│   |   ├── communication.py     # Implementation of communication among participants   
│   |   ├── fed_runner.py        # The runner for building and running an FL course
│   |   ├── ... ..
│   ├── cv                       # Federated learning in CV        
│   ├── nlp                      # Federated learning in NLP          
│   ├── gfl                      # Graph federated learning          
│   ├── autotune                 # Auto-tunning for federated learning         
│   ├── vertical_fl              # Vartical federated learning         
│   ├── contrib                          
│   ├── main.py           
│   ├── ... ...          
├── scripts                      # Scripts for reproducing existing algorithms
├── benchmark                    # We release several benchmarks for convenient and fair comparisons
├── doc                          # For automatic documentation
├── enviornment                  # Installation requirements and provided docker files
├── materials                    # Materials of related topics (e.g., paper lists)
│   ├── notebook                        
│   ├── paper_list                                        
│   ├── tutorial                                       
│   ├── ... ...                                      
├── tests                        # Unittest modules for continuous integration
├── LICENSE
└── setup.py
```

## 部署文档

We provide an end-to-end example for users to start running a standard FL course with FederatedScope.

### Step 1. clone

First of all, users need to clone the source code and install the required packages (we suggest python version >= 3.9).

```bash
git clone https://github.com/LuHyOcean/federatedscope.git
cd federatedscope
```
#### Step 2. 环境配置 （ Use Conda ）

We recommend using a new virtual environment to install FederatedScope:

```bash
conda create -n fs python=3.9
conda activate fs
```

If your backend is torch, please install torch in advance ([torch-get-started](https://pytorch.org/get-started/locally/)). For example, if your cuda version is 11.3 please execute the following command:

```bash
conda install -y pytorch=1.10.1 torchvision=0.11.2 torchaudio=0.10.1 torchtext=0.11.1 cudatoolkit=11.3 -c pytorch -c conda-forge
```

For users with Apple M1 chips:
```bash
conda install pytorch torchvision torchaudio -c pytorch
# Downgrade torchvision to avoid segmentation fault
python -m pip install torchvision==0.11.3
```

Finally, after the backend is installed, you can install FederatedScope from `source`:

##### From source

```bash
# Editable mode
pip install -e .

```

Now, you have successfully installed the minimal version of FederatedScope. 

#### Step 3. 医学图像分割实例 （ UNet_Drive ）

```shell
python federatedscope/main.py --cfg scripts/unet_drive_scripts/UNet.yaml
```

运行shell后，输出和日志的路径`exp/FedAvg_UNet_on_file_lr0.01_lstep1`。记录模型参数，模型性能，输出
