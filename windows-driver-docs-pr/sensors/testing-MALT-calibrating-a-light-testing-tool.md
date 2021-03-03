---
title: '校准光和彩色测试工具 (MALT) '
author: windows-driver-content
description: 本主题提供有关如何将 MALT (Microsoft 环境光线工具) 校准的说明。
ms.assetid: d045b771-b536-457c-897b-ecb6517bf0a8
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: da6d93bf84b85d3824f95320b7a56e32845cbd35
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101751941"
---
# <a name="calibrating-a-light-testing-tool-malt"></a>校准轻型测试工具 (MALT) 

彩色传感器通常需要校准。 校准是将传感器正在读取哪些值与环境中观测到的值对齐的过程。 本文档将指导你完成使用颜色计量器/显示读取器中的已知值校准 MALT 时所需的矩阵数学，以创建适当的校准矩阵。 对于环境颜色传感器和屏幕颜色传感器，必须执行 MALT 校准。

## <a name="step-1-acquire-known-values"></a>步骤1：获取已知值

已知的颜色值是任何校准过程的关键，并且来自已经校准的传感器，并具有正确的值。 对于图1中的三角形的三个主要颜色点，具有已知的值，在本文档结束时，我们可以创建一个矩阵，以便我们的原始值符合这些值。

可以通过多种方式来校准你的设备。 在本文档中，我们将使用手持式外部校准的设备（如 [I1Display Pro](https://www.xrite.com/categories/calibration-profiling/i1display-pro) ）来收集这些值，以捕获 XYZ 值和三个彩色光源，表示红色、绿色和蓝色。 任何具有可验证的正确值 (如现有校准 PC) 的设备都可用于查找这些数字。 这些 XYZ 值应绕0-100 到最有效的范围。 此操作用于显示红色、蓝色显示和绿色显示。 

![校准视觉对象](images/calibration-red.png)

按如下所示将观察到的值放入3x3 矩阵。 接下来，必须通过将 MALT 指向您收集的已知值的相同显示颜色来收集原始值。

![Srgb](images/srgb.png)

## <a name="step-2-acquire-raw-values-using-maltutilexe"></a>步骤2：使用 MALTUtil.exe 获取原始值

原始值或 uncalibrated 值是在应用任何数学或校准之前，来自当前 uncalibrated MALT 颜色传感器的值。 

通过将 MALT 指向您收集的已知值的相同显示颜色来收集这些值。 此步骤非常重要，并使公式可靠。 通过发送命令 ```/readRawAmbient``` 或 MALTUtil.exe 来读取 uncalibrated 值 ```/readRawScreen``` 。 此操作用于显示红色、蓝色显示和绿色显示。 XYZ 值应绕0-1 到最有效的范围。 如果数字不在此范围内，请按 Arduino 上的重置按钮，然后重试。 如下所示，将这些值放入3x3 矩阵。

![Srgb](images/rrgb.png)

## <a name="step-3-transform-the-matrices"></a>步骤3：转换矩阵

使用下面的公式和刚构建的矩阵生成校准矩阵 K。 S 是已知值的3x3 矩阵，R 是 uncalibrated 值的3x3 矩阵，R<sup>T</sup> 是矩阵 R 的换位。

![校准公式](images/calibration.png)

[单击此处查找 EXCEL 电子表格](images/CalibrationWorkbook.xlsx)

K 是一个3x3 矩阵，以便： 

![校准证明](images/calibration-proof.png)

这样一来，我们就可以使用 K 作为在固件中编程的静态矩阵，在将其输出到串行输出之前，我们将运行所有原始颜色数据。

## <a name="step-4-using-maltutilexe"></a>步骤4：使用 MALTUtil.exe

生成并验证校准矩阵后，应将其添加到固件，以便将 MALT 的彩色传感器视为已校准。 使用 MALTUtil.exe 可以将所有九个值从矩阵 K 传递到内存中，以便 MALT 可以通过校准的矩阵运行其原始编号。

MALTutil.exe 具有两种校准模式： ```/calibrateScreen``` 和 ```/calibrateAmbient``` 。 选取要 (屏幕或环境) 校准的传感器，并确保在命令窗口中键入正确的传感器。

命令后跟9个以空格分隔的浮点数。 这些数字来自校准矩阵 K，应按以下顺序输入： X1、X2、X3、Y1、Y2、Y3、Z1、Z2、Z3。

例如，如果 ![校准示例](images/calibration-example.png) 要校准环境传感器，需使用以下命令：
```cmd
MALTUtil.exe /calibrateAmbient 23.516 -74.312 402.104 3.716 102.003 95.664 182.669 3.844 40.892
```

输入已知的原始信息后，以上 Excel 工作表将为您输出此命令。 


![图 1](images/chromaticity-diagram.png)
