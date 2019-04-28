---
title: 测试自动亮度
author: windows-driver-content
description: 本主题介绍如何通过使用 MALT （Microsoft 环境光工具） 工具来测试自动亮度。
ms.assetid: 0ca1a07e-ab4d-47d1-b6ab-a1aa02ee3ee6
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 173a315d7ea4f0745cae80f6a203650fd7f0f3e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345143"
---
# <a name="testing-auto-brightness"></a>测试自动亮度

本主题介绍如何通过使用 MALT （Microsoft 环境光工具） 工具来测试自动亮度。 自动或自适应亮度是指在响应环境光线传感器读取系统会自动设置的屏幕亮度。 

## <a name="set-up"></a>设置

通读本主题[构建 Light 测试工具 (MALT)](testing-MALT-building-a-light-testing-tool.md)以确保已满足测试的要求。

### <a name="configuring-the-sut-manually"></a>手动配置 SUT

我们强烈建议你使用**MALT_SUT_Setup.bat**设置 MALT 和待测系统 (SUT)。 针对透明度和旧版目的提供了 MALT 和 SUT 的手动设置的以下说明。

1. 请确保 SUT 具有环境光线传感器 (ALS)。 若要了解您的 PC 是否在具有 ALS**显示**设置下**亮度和颜色**，寻找 **"亮度时自动更改照明的更改"** 复选框然后选择它以使用此功能。
2. 请确保屏幕将不关闭在测试期间。 若要调整 Windows 10 中的睡眠设置，请转到**启动**，然后选择**设置**  > **系统** > **电源和睡眠**. 下**屏幕**，更改**电池电源，将关闭后**到**从不**并**接通，关闭后**到**永远不会**。
3. 请确保你的设备将不会在测试期间进入睡眠状态。 若要调整 Windows 10 中的睡眠设置，请转到**启动**，然后选择**设置**  > **系统** > **电源和睡眠**. 下**睡眠**，更改**电池电源，PC 进入睡眠状态后**到**从不**并**接通，PC 进入睡眠状态后**到**永远不会**。
4. 若要减少测试可变性，请测试之前的 SUT 屏幕背景设置为纯白色。 选择**设置 > 个性化设置 > 背景**，然后将更改为背景下拉列表中 **"纯色"**。 单击**自定义颜色 > 更多**，将颜色十六进制值为`FFFFFF`。 您的桌面背景将变为纯白色。
5. 请确保卷已 SUT 上。 当完成测试，以通知它已完成的长时间运行时，应用程序将声音播放。

## <a name="automatic-brightness-test-procedures"></a>自动亮度测试过程

### <a name="get-ambient-light-response-curve"></a>获取环境光线响应曲线

**使用[SensorExplorer](https://aka.ms/sensorexplorer)应用 （推荐）**

1. 打开 SensorExplorer，然后单击**MALT**左侧菜单栏上。

![SensorExplorer MALT 页](images/SensorExplorerMALT.png)

2. 通过单击来验证连接**传感器数据** > **获取环境的亮度**。 如果已正确设置 MALT，将显示正确的 lux 值;否则为关闭应用程序中，请尝试重新上传 arduino 开发程序，然后检查串行监视器。
3. 下**运行测试**，单击**Take 自动亮度曲线**。 
4. 选择用于保存.csv 文件的位置。
5. 指定在测试开始前的等待时间。 这意味着让你有时间将传感器放在系统上。
6. 请等待。 此测试将需要大约 5 到 10 分钟。 测试调整到其最大亮度，大约是 0 到 2600年环境 lux 一系列从 0 光的亮度。
7. 在测试完成后，将自动向保存输出`autoBrightness.csv`和将播放声音通知您已完成测试。

**使用 MALTUtil.exe**

1. 通过运行验证的连接`MALTUtil.exe /screenLux`从 cmd。 如果 MALT 正确的设置，将显示正确的 lux 值，否则为命令将挂起或显示`No Arduino devices connected to the system`。
2. 在 SUT 上运行`MALTUtil.exe /autoCurve 30`中 cmd。 30 指 30 的第二个等待，然后在测试开始-这意味着让你有时间将传感器放在系统上。 如果需要更长 （或更短） 不是 30 秒来移动您周围的安装程序中的任何内容之前测试开始时，相应地调整数。
3. 请等待。 此测试将需要大约 5 到 10 分钟。 测试调整到其最大亮度，大约是 0 到 2600年环境 lux 一系列从 0 光的亮度。
4. 在测试完成后，将自动向保存输出`autoBrightness.csv`和将播放声音通知您已完成测试。

### <a name="open-the-results-in-microsoft-excel"></a>在 Microsoft Excel 中打开结果

1. 打开`autoBrightness.csv`在 Microsoft Excel 中。 本指南假定你使用 Microsoft Excel 2016。 如果使用不同版本，可能需要调整这些步骤。
2. 单击**文件** > **导出** > **更改文件类型**。 文件类型更改为.xlsx。 这将允许你创建并保存您的数据的可视化效果。
3. 在文档中，你将看到三个列： 

| 浅级别 | 环境 Lux  | 屏幕 Lux |
|-----|----|----|
| 最小值浅级别的 MALT 程序设置 | 最小环境 lux 值度量由 MALT 环境光线传感器 | 通过 MALT 屏幕光线传感器测量的相应屏幕 lux 值 |
| 最大浅级别的 MALT 程序设置 | 最大环境 lux 值由 MALT 环境光线传感器度量 | 通过 MALT 屏幕光线传感器测量的相应屏幕 lux 值 |

### <a name="visualize-the-results"></a>将结果可视化

如果使用 Microsoft Excel 2016 之外的某个程序，这些步骤可能会有所不同。

1. 在 Microsoft Excel.xlsx 文件中，选择包含数据的两个列："环境 Lux"和"屏幕上 Lux"。
2. 单击**插入** > **插入 （X，Y） 的散点图或气泡图** > **直接折线散点图** 

![插入散点图](images/insertScatter1.png)

现在可以自动亮度响应曲线由 MALT 度量的可视表示形式。

### <a name="interpret-the-results"></a>解释结果

您必须手动检查结果自行或与工程团队负责自动亮度曲线。 下面是一些要考虑的事项： 

1. 由 MALT 度量结果与预期的环境光线响应曲线在 BIOS 中定义匹配？ 
2. 环境光线响应曲线中是否有足够的步骤？ 将向用户明显的曲线具有几个点，因为它们调整亮度。
3. 是在较低曲线末尾的步骤小于末尾更高版本？ 亮度更改是在较低亮度更明显。 请考虑添加更频繁的曲线点更小的步骤与在较低的亮度百分比。

请参阅[本白皮书](https://docs.microsoft.com/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update)有关 Microsoft 的完整指导集成光线传感器和环境光线响应曲线。