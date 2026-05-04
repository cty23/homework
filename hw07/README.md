数据集统计
来源：Chest X-Ray Images (Pneumonia)

训练集 (Train): XXX 张 (Normal: XX, Pneumonia: XX)

验证集 (Val): XXX 张 (从原始训练集按 8:2 划分)

测试集 (Test): 624 张

模型结构与超参数
模型类型: 卷积神经网络 (CNN)

结构简述: 3个卷积层（包含 ReLU 激活与最大池化） + 全连接层 + Dropout 层 (0.5)

优化器: Adam

学习率: 1e-4

Batch Size: 32

Loss: Binary Crossentropy

结果分析 (任务二必答)
指标分析: 观察测试集的 Recall（召回率）。通常肺炎识别的 Recall 会很高，这意味着模型能有效捕捉大部分患者。

医学意义: 在临床中，召回率优于准确率。漏诊（假阴性）会导致患者延误治疗，风险极大；而误诊（假阳性）可通过二次筛查纠正。

数据增强: 缓解了模型在小规模医学数据集上的过拟合问题，使验证集曲线更加平滑。
