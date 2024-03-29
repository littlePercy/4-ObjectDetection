# 关于目标检测的知识

![faster-RCNN](https://user-images.githubusercontent.com/52816016/196070512-5094be94-8d19-4dee-893b-550fa4368ff8.png)

目标检测领域的深度学习算法可以分为两类，一阶段算法代表为YOLO，二阶段算法代表为R-CNN。阐述一下二阶段算法和一阶段算法的区别，二阶段算法首先生成候选区域（提议区域），然后针对候选区域进行筛选和预测。一阶段算法并没有单独的步骤用来生成候选区域，而是将候选区域的生成、筛选与预测同步进行。

R-CNN 中文名字是区域提议卷积网络，其发展大体经历了R-CNN、Fast R-CNN、Faster R-CNN到Mask R-CNN的过程。每一种新模型都是在旧模型的基础上优化改善而得。总体来说优化的目的都是在于，提高模型的计算速度，以及优化模型的计算精读。

R-CNN大体经过了以下步骤：1.通过选择性搜索算法得到大量提议区域。2.针对每一个提议区域使用卷积网络提取特征，计算特征图。3.针对每一个特征图训练SVM实现类别预测。4.针对每一个特征图训练边框回归，实现边框坐标偏移量预测。

Fast R-CNN针对于R-CNN中存在的大量卷积计算进行了优化。Fast R-CNN首先针对全图进行卷积网络特征提取，然后同样使用选择性搜索算法生成大量提议区域，使用RoIPooling算法针对每一个提议区域从全图特征中挑选特征值，并调整维度。标签值与偏移量的预测与R-CNN相同。

Faster R-CNN针对提议区域的生成方式进行了修改。Faster R-CNN采用RPN网络的方式生成提议区域，接受全图特征图作为输入，筛选提议区域，极大减少了提议区域的生成数量。
Mask R-CNN为了实现像素级别的分类进行了优化。使用RoIAlign代替RoIPooling，将多尺寸提议区域进行特征对齐，原RoIPooling算法无法支持高精度的像素级别的图像分类。除了标签值和边界框偏移量的预测以外，单独开设一个分支通过全卷积网络实现像素级别分类。

![Mask-RCNN](https://user-images.githubusercontent.com/52816016/196070339-45ab11ff-0f5e-4977-b1de-c898536a4a31.png)
