---
title: 构建测试工具 (MALT) 的光
author: windows-driver-content
description: 本主题提供有关如何使用 MALT （Microsoft 环境光工具） 的说明作为测试解决方案的光。
ms.assetid: d045b771-b536-457c-897b-ecb6517bf0a8
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 81f5d4866cc3244a94a1094ec8fb5a01b21471f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345177"
---
# <a name="building-a-light-testing-tool-malt"></a>构建测试工具 (MALT) 的光

本主题说明和要求提供有关如何使用 （以及构建如有必要） 以进行测试和校准屏幕亮度的工具。 MALT (**M**icrosoft **A**mbient **L**右键**T**ool) 供参考。 

请利用你的测试解决方案的想法和理念按这些说明进行操作。 微型控制器 API 发布，以便进一步利用测试已发布的 HLK 中和其他位置。 你的反馈将帮助改进本指南。

![malt 设备](images/MALT.png)

## <a name="prerequsites"></a>先决条件

本指南假定编程，和焊接，电子设备，在具有基本知识。

## <a name="components"></a>组件

您将需要以下组件。

* [Microcontroller](https://www.arduino.cc/en/Main/arduinoBoardMega)
* [足够多的已校准的光源 / 范围](https://www.superbrightleds.com/moreinfo/led-panel-light/square-12v-led-panel-light-fixture-1ft-x-1ft-35w/2184/)
* [光源的电源](https://www.superbrightleds.com/moreinfo/led-panel-light/square-12v-led-panel-light-fixture-1ft-x-1ft-35w/2184/#tab/PowerSupplies/subtab/powersupply)
* [数字模拟转换器 (DAC) 到](https://www.microchip.com/wwwproducts/en/MCP4821)
* 2 [Ambient 光传感器 （例如 TI OPT3001 或更高）](https://www.ti.com/product/OPT3001)
* 2[颜色传感器](https://www.digikey.com/product-detail/en/ams/TCS34727FN/TCS34727FNCT-ND/3737677)
* [浅机箱](#light-enclosure)

## <a name="instructions"></a>说明

### <a name="step-1---assemble-light-enclosure"></a>步骤 1-组装 light 机箱

控制灯公开给待测系统 (SUT) 是关键准确地进行测试。 机箱必须与正在使用浅色面板和 SUT 相匹配。 这将包括 top，用于可控制光源和为 SUT 下方留出空间 aperture 具有的框。

![浅机箱](images/box.png)

我们使用的便携式计算机的机箱是 16"x 16"x12"，使用 10 个"x 10"aperture 顶部的机箱。  [模型](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Schematics/enclosure)可以 3D 打印。 

#### <a name="light-enclosure-tips"></a>浅机箱提示

一个有效的浅机箱将提供从受控光源和不是环境下测试面板 （或设备） 上的光线强制转换将在其中没有影响浅色环境。 浅框的示例如下。

* [自定义 3D 打印的用例](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Schematics/enclosure)
* [存储 Tote](http://www.sterilite.com/SelectProduct.html?id=955&ProductCategory=182&section=1)
* 纸板框

机箱与主机箱需要有足够的 SUT，并从外部浅影响浅装置可以置于顶部或装载主机箱中删除它。

如果浅装置框外部装载 （在最前面），请确保 aperture 将容纳装置，并提供足够轻度到中 SUT 光线传感器。

#### <a name="assembly-tips"></a>程序集的提示

* 如果程序集需要是粘附或磁带，则我们建议使用粘附或[粗面纸黑色 gaffer 磁带](https://en.wikipedia.org/wiki/Gaffer_tape)。
* 检查机箱与工作图面放置在机箱齐平。 应存在任何外部浅泄漏。
* 使用从 MALT （和浅机箱中的没有 SUT） 以确定是否存在入机箱的外部环境光线泄漏传感器。
* 如果光源需要 aperture，请使用大小适当的漏洞，使你光可以而无需故障或泄露 light 鼠标框之上。

### <a name="step-2---assemble-sensors"></a>步骤 2-组合传感器

MALT 使用两个光线传感器 （一个来测量屏幕亮度），另一个用于测量环境亮度和两个颜色传感器 （一个来测量屏幕颜色），另一个用于度量值的环境颜色。 若要同时实现这些操作，将这些过程，这样一个光线传感器和一种颜色传感器背其他两个传感器。 当屏幕传感器正面临着向下 （坐在屏幕上），其他传感器正面临着向上来测量环境光线。

![传感器远程测试机组](images/sensor.png)

连接到电源供应的 LED 指示灯面板并将其连接到 DAC。 微型控制器必须能够控制发送到浅色面板以便控制其强度，实现使用 DAC 的电压。 我们使用下面显示了该工具如何对连接的示意图。 可以在传感器 PCB KiCad 项目中找到更多详细信息。

![传感器示意图](images/SensorPCB.png)


### <a name="step-3---connect-the-microcontroller"></a>步骤 3-连接微型控制器

将传感器连接到微型控制器和到 PC 微控制器。 对于我们的目的，我们提供控制测试作为待测系统 (SUT) 相同的 PC。

下图显示了如何各个组成部分 MALT 连接。

![框图](images/BlockDiagram.png)

通过 MALT PCB，我们将能够连接到传感器 PCB arduino 开发板和光源。 可以在 MALT PCB KiCad 项目中找到更多详细信息。

![MALT 示意图](images/MaltPCB.png)

### <a name="step-4--start-testing"></a>步骤 4 开始测试

请参阅[测试系统亮度响应](testing-MALT-system-brightness-response.md)有关设置和使用 MALT 只收集组的详细信息。

#### <a name="test-scenarios-to-cover"></a>测试方案，以涵盖

* [测试自动亮度](testing-MALT-auto-brightness.md)

* [测试手动亮度](testing-MALT-manual-brightness.md)

* [测试系统方案](testing-MALT-system-scenarios.md)

请参考  
[微型控制器命令](testing-MALT-microcontroller-commands.md)MALT 有关创建自定义测试时使用的 api。