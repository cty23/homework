# Chest X-Ray Pneumonia Detection (CNN)

这是一个基于深度学习的医疗辅助诊断项目，使用卷积神经网络 (CNN) 对胸部 X 光图像进行自动分析，识别是否存在肺炎。

## 模型训练表现 (Training Performance)

模型在训练过程中表现出稳健的收敛性，验证集指标与训练集高度同步，有效避免了严重的过拟合。

| 阶段 | 准确率 (Accuracy) | 损失值 (Loss) |
| :--- | :--- | :--- |
| **训练集 (Training)** | 93.75% | 0.1741 |
| **验证集 (Validation)** | 93.48% | 0.1448 |

---

## 测试集评估结果 (Evaluation)

模型在完全未见过的测试数据上进行了评估，其核心指标如下：

### 1. 分类性能报告 (Classification Report)

| 类别 (Class) | 精确率 (Precision) | 召回率 (Recall) | F1-Score |
| :--- | :--- | :--- | :--- |
| **Normal (正常)** | 0.94 | 0.62 | 0.75 |
| **Pneumonia (肺炎)** | 0.81 | **0.98** | 0.89 |
| **平均/总计 (Overall)** | 0.86 | 0.84 | 0.84 |

### 2. 核心结论分析
*   **极高的肺炎检出率 (Recall = 0.98)**：在 624 张测试图像中，模型几乎识别出了所有的肺炎病例。对于医疗诊断而言，低漏诊率（高召回率）至关重要。
*   **误诊权衡**：目前正常类别的召回率较低（0.62），这意味着模型倾向于将一些模糊的正常影像判定为肺炎（保守诊断）。这在临床初筛阶段是可以接受的，能确保患者得到进一步检查。

---
## 技术实现细节

*   **架构**: 多层卷积神经网络 (CNN)，包含 Convolutional 层、MaxPooling 层以及 Dropout 正则化层。
*   **图像处理**: 
    *   输入尺寸：根据预处理设定进行缩放。
    *   数据增强：使用了 `ImageDataGenerator` 进行随机旋转、缩放和水平翻转。
*   **优化器**: Adam Optimizer。
*   **损失函数**: Binary Crossentropy (二元交叉熵)。

---

##  快速开始

### 环境依赖
- Python 3.x
- TensorFlow / Keras
- NumPy
- Matplotlib / Seaborn (用于结果可视化)

### 预测示例
```python
import tensorflow as tf

# 加载模型
model = tf.keras.models.load_model('your_model.h5')

# 进行预测
prediction = model.predict(preprocessed_image)
print("诊断结果:", "肺炎" if prediction[0] > 0.5 else "正常")
