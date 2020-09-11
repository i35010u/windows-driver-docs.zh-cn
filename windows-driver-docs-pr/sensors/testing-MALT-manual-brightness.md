---
title: 测试手动亮度
author: windows-driver-content
description: 本主题介绍如何使用 MALT (Microsoft 环境光线工具) 工具测试手动亮度。
ms.assetid: 1a7dd439-2634-49ae-8b0c-1dec843b34d7
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 44aa5449951aecdb48bb9d4383feffa5ed2a869e
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010287"
---
# <a name="testing-manual-brightness"></a>测试手动亮度

本主题介绍如何使用 MALT (Microsoft 环境光线工具) 工具测试手动亮度。 手动亮度是指由用户 *手动* 设置的屏幕亮度。

## <a name="set-up"></a>设置

通读 [ (MALT) 的构建轻型测试工具 ](testing-MALT-building-a-light-testing-tool.md) 主题，以确保满足测试的要求。

### <a name="configuring-the-sut-manually"></a>手动配置 SUT

我们强烈建议你使用 [MALT_SUT_Setup.bat](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Code/Scripts) 来设置 MALT，以及 (SUT) 测试的系统。 以下有关手动设置 MALT 和 SUT 的说明仅用于透明度和传统用途。

1. 如果使用的是具有环境光线传感器的计算机，则需要关闭自适应亮度才能测试手动亮度。 若要查明你的电脑是否支持此功能，请在 " **显示设置**" 中的 " **亮度和颜色**" 下查找 **"光线变化时自动更改亮度"** 复选框，然后取消选中以关闭此功能。 如果该复选框不存在，则无需执行其他操作。
2. 请确保在测试过程中屏幕不会关闭。 若要在 Windows 10 中调整睡眠设置，请单击 "**开始**"，然后选择 "**设置**" "   >  **系统**  >  **电源 & 睡眠**"。 在 "**屏幕**" 下，更改**电池电源，在接通电源后**关闭，**并在****接通**电源后关闭 **。**
3. 确保在测试过程中设备不会进入睡眠状态。 若要在 Windows 10 中调整睡眠设置，请单击 "**开始**"，然后选择 "**设置**" "   >  **系统**  >  **电源 & 睡眠**"。 在**睡眠状态**下 **，使用电池电量改变，pc 进入睡眠状态后进入睡眠状态** **，pc 进入睡眠状态后进入睡眠状态** **。** **Never**
4. 若要减少测试可变性，请在测试之前将 SUT 的屏幕背景设置为纯白。 选择 " **设置" > 个性化 > "背景**"，然后将 "背景" 下拉列表更改为 **"纯色"**。 单击 " **自定义颜色 > 更多** "，并将 "十六进制值" 更改为 `FFFFFF` 。 这会将桌面背景更改为纯白。
5. 请确保在 SUT 上已打开该卷。 当长时间运行的测试完成时，应用程序将发出声音，通知您已完成。

## <a name="manual-brightness-test-procedures"></a>手动亮度测试过程

### <a name="test-rig-placement"></a>测试远程测试机组

1. 将屏幕上的 MALT 屏幕光线传感器置于空白区域。 可能需要将电脑侧向放置或将 MALT 屏幕光线传感器放到屏幕上。

> [!NOTE] 
> 此测试不需要灯具机箱、灯具面板和 MALT 环境光源传感器。

### <a name="get-manual-light-curve"></a>获取手动细曲线

**使用 MALTUtil.exe**

1. 在 SUT 上， `MALTUtil.exe /manualLux 30` 在 cmd 中运行。 30表示在测试开始之前30秒等待。 这是为了让你有时间将传感器置于系统上。 如果需要更长的 (或更短的) ，以便在测试开始之前在安装中移动任何内容，请相应地调整此数字。
2. 再. 这将需要大约2分钟。 测试会将 SUT 上的屏幕亮度调整为0% 到100%，并读取屏幕亮度。
3. 测试完成后，输出将自动保存到， `manualBrightness.csv` 然后播放一则声音，通知您测试已完成。

### <a name="open-the-results-in-microsoft-excel"></a>在 Microsoft Excel 中打开结果

1. `manualBrightness.csv`在 Microsoft Excel 中打开。 本指南假定你使用的是 Microsoft Excel 2016。 如果你使用的是其他版本，则可能需要调整这些步骤。 
2. 单击 "**文件**  >  **导出**  >  **更改文件类型**"。 将文件类型更改为 .xlsx。 这将允许您创建和保存数据的可视化效果。
3. 在文档中，将看到两个列： 

| 亮度百分比 | 屏幕 Lux       |
|----|-----|
| 0%  | 由 MALT 屏幕光线传感器度量的屏幕 lux 值 |
| 100%  | 由 MALT 屏幕光线传感器度量的屏幕 lux 值 |

### <a name="visualize-the-results"></a>可视化结果

如果你使用的程序不是 Microsoft Excel 2016，这些步骤可能会有所不同。

1. 在 Microsoft Excel .xlsx 文件中，选择包含数据的两个列： "亮度百分比" 和 "Screen Lux"。
2. 单击 "**插入**  >  ** (X、Y) 的插入散点图或气泡图**  >  **散点（带直线**） 

![插入散点图](images/insertScatter2.png)

现在，您可以直观地表示由 MALT 测量的手动亮度响应曲线。

### <a name="interpret-the-results"></a>解释结果

您必须自行或由您的工程团队负责手动亮度曲线手动检查结果。 以下是一些需要考虑的事项： 

1. MALT 度量的结果是否与 BIOS 中手动亮度曲线的预期定义匹配？
2. 手动亮度曲线是否有足够的步骤？ 当用户调整亮度时，具有几个点的曲线将对用户很明显。
3. 曲线的底部的步骤是否小于曲线的最低端？ 亮度变化更明显降低亮度。 请考虑在亮度百分比较低的情况下添加更频繁的曲线点。

请参阅 [此白皮书](/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update) ，了解有关如何集成光源传感器和环境光线响应曲线的 Microsoft 完整指导。