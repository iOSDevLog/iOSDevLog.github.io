---
layout: post
title: "Day 14: ARKit+Swift 版本的机器学习算法 k-NN"
author: iosdevlog
date: 2025-09-14 23:54:24 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485769&idx=1&sn=e9b6c030acac66bf7d544aa244a6ca8b&chksm=f95c92cece2b1bd829c0f75767b64652dc724ed3586bbb17bd2eaf48f5737f49fc7fac630c7e#rd

维基介绍

在模式识别领域中，最近邻居法（KNN算法，又译K-近邻算法）是一种用于分类和回归的非参数统计方法[1]。在这两种情况下，输入包含特征空间（Feature Space）中的k个最接近的训练样本。

在k-NN分类中，输出是一个分类族群。一个对象的分类是由其邻居的“多数表决”确定的，k个最近邻居（k为正整数，通常较小）中最常见的分类决定了赋予该对象的类别。若k = 1，则该对象的类别直接由最近的一个节点赋予。

在k-NN回归中，输出是该对象的属性值。该值是其k个最近邻居的值的平均值。

最近邻居法采用向量空间模型来分类，概念为相同类别的案例，彼此的相似度高，而可以借由计算与已知类别案例之相似度，来评估未知类别案例可能的分类。

K-NN是一种基于实例的学习，或者是局部近似和将所有计算推迟到分类之后的惰性学习。k-近邻算法是所有的机器学习算法中最简单的之一。

无论是分类还是回归，衡量邻居的权重都非常有用，使较近邻居的权重比较远邻居的权重大。例如，一种常见的加权方案是给每个邻居权重赋值为1/ d，其中d是到邻居的距离。[注 1]

邻居都取自一组已经正确分类（在回归的情况下，指属性值正确）的对象。虽然没要求明确的训练步骤，但这也可以当作是此算法的一个训练样本集。

k-近邻算法的缺点是对数据的局部结构非常敏感。本算法与K-平均算法（另一流行的机器学习技术）没有任何关系，请勿与之混淆。

ARKit + Swift + k-NN 实现

创建 KNN 类（结构体 struct也行，我是为了 与 sklearn尽量一致）。

/// KNN

public struct KNN<Feature, Label: Hashable> {

}

属性

/// Number of neighbors to use by default for :meth:`kneighbors` queries

privatevark:Int

/// Data set

privatevarX=[Feature]()

/// Target values

privatevary=[Label]()

/// distance

privateletdistanceMetric:(_x1:Feature,_x2:Feature)->Double

/// draw radius for debug

publicvardebugRadiusCallback:(([Double])->())?=nil

数据：

k

: 指定取 k 个最接近的训练样本

X

: 样本特征 （数组）一般要传数组的数组

y

: 样本标签 （数组）

辅助：

distanceMetric

: 用来计算距离的函数

debugRadiusCallback

: 调度时候用，主要是画出最近的 k 个样本范围

方法

/// constructorLabels for xTest

///

/// - Parameters:

///   - k: k

///   - distanceMetric: distance

publicinit(k:Int,distanceMetric:@escaping(_x1:Feature,_x2:Feature)->Double)

/// train

///

/// - Parameters:

///   - X: Training set

///   - y: Target values

publicmutatingfuncfit(X:[Feature],y:[Label])

/// Labels for xTest

///

/// - Parameter XTest: Test set

/// - Returns: Target values

publicfuncpredict(XTest:[Feature])->[Label]

init()

: 构造函数 需要预先决定 k和距离计算方法

fit()

: 拟合目标函数，kNN 不需要拟合，只要记下数据即可

predict()

: 预测给定的特征，返回对应的标签

距离计算

publicstructDistance{

/// Helper function to calculate euclidian distance

///

/// - Parameters:

///   - x0: source coordinate

///   - x1: target coordinate

/// - Returns: euclidian distance

publicstaticfunceuclideanDistance(_x0:[Double],_x1:[Double])->Double

// Convenience

publicstaticfunceuclideanDistance()->(([Double],[Double])->Double){

return{self.euclideanDistance($0,$1)}

}

这里使用 欧式距离（Euclidean Distance）

KNN 使用：

functestKNN(){

letkNN=KNN<Double,Int>(k:3)

letX=[[1.0],[2],[3],[4]]

lety=[0,0,1,1]

kNN.fit(X,y)

letlabel=kNN.predict([[1.2],[3]])

XCTAssertEqual([0,1],label)

}

显示 2 维

enumMLStep:Int{

casetrain

casepredict

}

enumGeometryType:Int{

casebox

casepyramid

casesphere

casecylinder

casecone

casetube

casetorus

...

}

MLStep

： 分成 训练 和 预测 ，训练一次，可以一直预测。

GeometryType

： 定义几种形状，这里定义给 ARKIT使用的

KNNViewController

classKNNViewController:UIViewController{

letradius:CGFloat=5

publicvarX:[[Double]]=[]

publicvary:[GeometryType]=[]

publicvarXTest:[[Double]]=[]

publicvaryTest:[GeometryType]=[]

publicvarradiuses:[Double]=[]{

didSet{

for(center,r)inzip(XTest,radiuses){

drawCircle(center:CGPoint(x:center[0],y:center[1]),radius:CGFloat(r))

}

}

}

publicvarpredictLayers:[CALayer]=[]

varmodel=KNN<[Double],GeometryType>(k:1,distanceMetric:Distance.euclideanDistance())

@IBOutletweakvarkNNPickerView:UIPickerView!

@IBOutletweakvarpanelView:UIView!

@IBOutletweakvartrainBarButtonItem:UIBarButtonItem!

varmlStep=MLStep.train{

didSet{

switchmlStep{

case.train:

trainBarButtonItem.title="train"

default:

trainBarButtonItem.title="predict"

}

}

}

...

}

添加 Layer到 panelView上实现类别，2D 只分了三个类别，分别用 方形（红），三角形（蓝），花形（绿）表示。

使用 alpha表示预测类别，以预测样本为中心画一个圈，圈内为最近的 k个样本。

funcdrawCircle(center:CGPoint,radius:CGFloat,alpha:CGFloat=0.1){

letr=self.radius+radius

letkNNCircleLayer=CAShapeLayer()

kNNCircleLayer.path=UIBezierPath(roundedRect:CGRect(x:center.x-r,y:center.y-r,width:r*2,height:r*2),cornerRadius:r).cgPath

kNNCircleLayer.fillColor=UIColor(red:0.1,green:0.1,blue:0.1,alpha:alpha).cgColor

kNNCircleLayer.borderColor=UIColor(red:0.8,green:0.8,blue:0.8,alpha:1).cgColor

kNNCircleLayer.borderWidth=1

panelView.layer.addSublayer(kNNCircleLayer)

}

圆内为 k个样本。

ARKit 实现

能 3D 展示多好，别急，下面就是用 ARKit实现的 3D 版本。

classARKNNViewController:UIViewController

基本实现和 ARKNNViewController类似。

funcdrawSphere(center:SCNVector3,radius:Float){

letgeometry=SCNSphere(radius:CGFloat(radius)+self.radius)

geometry.firstMaterial?.diffuse.contents=UIColor(red:0.1,green:0.1,blue:0.8,alpha:0.7)

letnode=SCNNode()

node.geometry=geometry

node.position=center

sceneView.scene.rootNode.addChildNode(node)

}

这是画最外面的范围球体，球体内为 k个样本。

视频

b站视频：https://www.bilibili.com/video/av48647681/

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_jpg/kIE7WtwNFTRXpbRibeoCD94DvJePGhnRztl1ABKicJQ0Y4yKkvlST4swuQxsR4unDhSasXZVcDzamiaJfQjPUFjBg/640?wx_fmt=other&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_jpg/kIE7WtwNFTRXpbRibeoCD94DvJePGhnRzmBQl1KbB9KNnj67icTbicJxlRCV39iaerZujTQjQI9uMUicCicgK7xh490Q/640?wx_fmt=other&from=appmsg&watermark=1#imgIndex=1)
