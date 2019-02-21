---
title: 测试手动亮度
author: windows-driver-content
description: 本主题介绍如何通过使用 MALT （Microsoft 环境光工具） 工具来测试手动亮度。
ms.assetid: 1a7dd439-2634-49ae-8b0c-1dec843b34d7
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3d81068012a347632138e0b23c93f2008136d4b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543200"
---
# <a name="testing-manual-brightness"></a>测试手动亮度

本主题介绍如何通过使用 MALT （Microsoft 环境光工具） 工具来测试手动亮度。 手动亮度是指屏幕亮度集*手动*用户。

## <a name="set-up"></a>设置

通读本主题[构建 Light 测试工具 (MALT)](testing-MALT-building-a-light-testing-tool.md)以确保已满足测试的要求。

### <a name="configuring-the-sut-manually"></a>手动配置 SUT

我们强烈建议你使用[MALT_SUT_Setup.bat](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Code/Scripts)设置 MALT 和待测系统 (SUT)。 透明度和兼容目的仅提供了用于手动设置 MALT 和 SUT 的以下说明。

1. 如果一台计算机将用于环境光线传感器，您需要为了测试手动亮度关闭自适应亮度。 若要了解您的 PC 是否支持此操作，请在**显示设置**下**亮度和颜色**，寻找 **"亮度时自动更改照明的更改"** 检查框中，然后再取消选中它以关闭此功能。 如果复选框不存在，不则需要任何进一步的操作。
2. 请确保屏幕将不关闭在测试期间。 若要调整 Windows 10 中的睡眠设置，请转到**启动**，然后选择**设置**  > **系统** > **电源和睡眠**. 下**屏幕**，更改**电池电源，将关闭后**到**从不**并**接通，关闭后**到**永远不会**。
3. 请确保你的设备将不会在测试期间进入睡眠状态。 若要调整 Windows 10 中的睡眠设置，请转到**启动**，然后选择**设置**  > **系统** > **电源和睡眠**. 下**睡眠**，更改**电池电源，PC 进入睡眠状态后**到**从不**并**接通，PC 进入睡眠状态后**到**永远不会**。
4. 若要减少测试可变性，请测试之前的 SUT 屏幕背景设置为纯白色。 选择**设置 > 个性化设置 > 背景**，然后将更改为背景下拉列表中 **"纯色"**。 单击**自定义颜色 > 更多**，将颜色十六进制值为`FFFFFF`。 您的桌面背景将变为纯白色。
5. 请确保卷已 SUT 上。 当完成测试，以通知它已完成的长时间运行时，应用程序将声音播放。

## <a name="manual-brightness-test-procedures"></a>手动亮度测试过程

### <a name="test-rig-placement"></a>测试远程测试机组放置

1. 纯色的白色区域中的屏幕上放置 MALT 屏幕光线传感器。 您可能需要将手机放 PC 或否则词缀 MALT 屏幕在屏幕上的光线传感器。

> [!NOTE] 
> 浅机箱、 浅面板和 MALT 环境光线传感器不需要为此测试。

### <a name="get-manual-light-curve"></a>获取手动浅曲线

**使用 MALTUtil.exe**

1. 在 SUT 上运行`MALTUtil.exe /manualLux 30`中 cmd。 在测试开始前 30 指 30 的第二个等待。 这意味着让你有时间将传感器放在系统上。 如果需要更长 （或更短） 不是 30 秒来移动您周围的安装程序中的任何内容之前测试开始时，相应地调整数。
2. 请等待。 这将需要大约 2 分钟。 测试是从 0 到 100%SUT 上的屏幕亮度调整，并读取屏幕亮度。
3. 在测试完成后，将自动向保存输出`manualBrightness.csv`和将播放声音通知您已完成测试。

### <a name="open-the-results-in-microsoft-excel"></a>在 Microsoft Excel 中打开结果

1. 打开`manualBrightness.csv`在 Microsoft Excel 中。 本指南假定你使用 Microsoft Excel 2016。 如果使用不同版本，可能需要调整这些步骤。 
2. 单击**文件** > **导出** > **更改文件类型**。 文件类型更改为.xlsx。 这将允许你创建并保存您的数据的可视化效果。
3. 在文档中，你将看到两个列： 

| 亮度百分比 | 屏幕 Lux       |
|----|-----|
| 0%  | 通过 MALT 屏幕光线传感器测量屏幕 lux 值 |
| 100%  | 通过 MALT 屏幕光线传感器测量屏幕 lux 值 |

### <a name="visualize-the-results"></a>将结果可视化

如果使用 Microsoft Excel 2016 之外的某个程序，这些步骤可能会有所不同。

1. 在 Microsoft Excel.xlsx 文件中，选择包含数据的两个列："亮度百分比"和"屏幕上 Lux"。
2. 单击**插入** > **插入 （X，Y） 的散点图或气泡图** > **直接折线散点图** 

![插入散点图](images/insertScatter2.png)

现在你已手动亮度响应曲线由 MALT 度量的可视表示形式。

### <a name="interpret-the-results"></a>解释结果

您必须手动检查结果自行或与工程团队负责手动亮度曲线。 下面是一些要考虑的事项： 

1. 由 MALT 度量结果是否匹配在 BIOS 中手动亮度曲线的预期的定义？
2. 手动亮度曲线中是否有足够的步骤？ 将向用户明显的曲线具有几个点，因为它们调整亮度。
3. 是在较低曲线末尾的步骤小于末尾更高版本？ 亮度更改是在较低亮度更明显。 请考虑添加更频繁的曲线点更小的步骤与在较低的亮度百分比。

请参阅[本白皮书](https://docs.microsoft.com/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update)有关 Microsoft 的完整指导集成光线传感器和环境光线响应曲线。