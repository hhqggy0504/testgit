# 一、机器学习&深度学习
## 1.1   相关规定   
    Machine Learning≈Looking for Function
    回归、分类、生成其他形式内容
    
    Supervised Learning——监督学习（需要label，耗费人工）
        -Self-supervised Learning——Pre-train+Downstream Task   
    Generative Adversarial Network（生成式对抗网络）
    Reinforcement Learning（强化学习）
    Explainable AI
    Model Attack
    Domain Adaptation
    Network Compression
    Life-long learning
    Meta learning≈Few-shot learning

## 1.2 机器学习基本概念
    找一个f函数
    三个任务：Regression回归，Classification分类，Strutured Learning
    
    过程
    1.猜测函数式大概模样：eg：Youtube y=b+wx1（依靠domain knowledge领域知识）——为一次线性
    2.Define Loss：Loss is a function of parameters（L(b,w)）——MAE/MSE/cross entroy   →→→  根据不同参数绘制出Loss等高线图error surface
    3.Optimization——w*,b*=argmin(w,b)L——  “Gradient Descent”
      ①选取一个w0初始值
      ②计算微分，（Negative-increse w；Positive-Decrease w（针对于只有w时候））————步伐大小取决于微分大小和n(learning rate)
       自己设定的参数为hyperparameters——————w1<--w0-n*微分=w0
      ③持续更新参数Updata w iteratively
      会有local minima问题（但说是假问题）

## 1.3 深度学习相关概念
    All Piecewise Linear Curves = constant + sum of a set of ...（激活）
    ----Sigmoid Function：y=1/(1+e^x)  ---->>>  cSigmoid(wx+b)  ---->>>可以用线性代数或者矩阵表示

    所有位置参数统称θ

    按照一个batch一个batch来更新参数，把所有都看过一遍叫做一个Epoch

    ReLU

## 1.4 torch相关用法
    torch训练和验证时候，要注意验证的时候要把梯度更新关掉

    torch.nn -> neural network
    torch.optim -> optimization algorithms
    torch.utils.data -> dataset,dataloader

    位置参数依赖于参数的位置顺序，传递参数值时必须按照函数定义中的顺序传递----*args 是用来表示函数接受任意数量的位置参数
    关键字参数通过参数名传递，不受位置影响，可以任意顺序传递参数值----**kwargs 则是用来表示函数接受任意数量的关键字参数
    
    nn.Sequential(连接起来，将所有层包装)
    cat可以连接起来维度（拼接）
![DNN](\pic\111.png)

## 2.1 深度学习

![DL0](\pic\img_4.png)

![DL1](\pic\img_5.png)

GPU   >>>>   矩阵运算

chain rule  >>>>>  链式法则
![DL2](\pic\img_6.png)

![DL3](\pic\img_7.png)

backward pass   >>>>      建立一个反向的neural network

1. 有序列表  
   1.1 有序列表  
   1.2 有序列表
2. ***有序列表***
3. 有序列表