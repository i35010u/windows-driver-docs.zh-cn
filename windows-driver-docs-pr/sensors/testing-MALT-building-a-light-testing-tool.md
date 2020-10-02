---
title: " (MALT) 构建轻型测试工具"
description: 了解如何构建 MALT (Microsoft 环境光线工具) ，用于测试和校准屏幕亮度。
ms.assetid: d045b771-b536-457c-897b-ecb6517bf0a8
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: e27fce09398d1fcb17c74f2ca95eb17bf607266d
ms.sourcegitcommit: 372464be981a39781c71049126f36891cb5d0cad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91645977"
---
# <a name="building-a-light-testing-tool-malt"></a> (MALT) 构建轻型测试工具

本主题提供有关如何使用 (和生成的说明和要求) 用于测试和校准屏幕亮度的工具。 MALT (**M**icrosoft **A**mbient **L**右键 **T**ool) 用于引用。

请使用这些说明来利用您的测试解决方案。 发布微控制器 API，以便进一步利用在 HLK 和其他位置发布的测试。 你的反馈将有助于改进本指南。

![malt 设备](images/MALT.png)

## <a name="prerequsites"></a>先决条件

本指南假定你在电子、编程和焊接方面具有基本知识。

## <a name="components"></a>组件

你将需要以下组件。

* [微控制器](https://store.arduino.cc/mega-2560-r3)
* [校准了足够范围/色谱的光源](https://www.superbrightleds.com/moreinfo/led-panel-light/square-12v-led-panel-light-fixture-1ft-x-1ft-35w/2184/)
* [用于光源的电源](https://www.superbrightleds.com/moreinfo/led-panel-light/square-12v-led-panel-light-fixture-1ft-x-1ft-35w/2184/#tab/PowerSupplies/subtab/powersupply)
* [将数字转换为模拟转换器 (DAC) ](https://www.microchip.com/wwwproducts/en/MCP4821)
* 2个 [环境光线传感器 (EX TI OPT3001 或更好) ](https://www.ti.com/product/OPT3001)
* 2 [彩色传感器](https://www.digikey.com/product-detail/en/ams/TCS34727FN/TCS34727FNCT-ND/3737677)
* [灯具机箱](#step-1---assemble-light-enclosure)

## <a name="instructions"></a>Instructions

### <a name="step-1---assemble-light-enclosure"></a>步骤 1-组装灯具机箱

控制公开给受测系统 (SUT) 是准确测试的关键。 机箱需要与正在使用的灯光面板和 SUT 匹配。 这将包含一个框，其中的口径位于其下方的可控制光源和空间。

![灯具机箱](images/box.png)

用于便携式计算机的机箱是 16 "x16" x12，机箱顶部有10个 "x10" 口径。  可以对 [模型](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Schematics/enclosure) 进行三维打印。

#### <a name="light-enclosure-tips"></a>轻型机箱提示

有效的光线箱将提供一个取证的光源环境，在此环境中，面板 (或设备) 在测试的光源环境将来自受控光源而不是环境。 下面是灯光方框的示例。

* [自定义三维打印事例](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Schematics/enclosure)
* [存储 Tote](https://www.sterilite.com/SelectProduct.html?id=955&ProductCategory=182&section=1)
* Cardboard 框

机箱必须足够大，可用于 SUT，并将其从外部光源中删除，光装置可以放置在机箱的顶部或装入机箱内。

如果光装置安装在机箱外 (顶部) 上，请确保口径可容纳装置，并向 SUT 中的光线传感器提供充足的光源。

#### <a name="assembly-tips"></a>程序集提示

* 如果 box 组件需要粘附或磁带，则建议使用胶水或 [粗糙黑色 gaffer 磁带](https://en.wikipedia.org/wiki/Gaffer_tape)。
* 检查机箱与机箱所在的工作图面是否齐齐。 不应存在外部轻型泄露。
* 使用 MALT (中的传感器，不使用灯具机箱) 中的 SUT 来确定机箱中是否存在外部环境光泄漏。
* 如果光源需要口径，请使用适当大小的孔，使光线可以在机箱上停留，而不会穿透或泄漏光。

### <a name="step-2---assemble-sensors"></a>步骤 2-组装传感器

MALT 使用两个光源传感器 (一个传感器来测量屏幕亮度，使用一个传感器来测量) 的环境亮度，并使用两个彩色传感器来测量屏幕颜色，将两个彩色传感器 (一个用于测量屏幕颜色，另一个用于测量环境颜色) 。 若要同时实现这些目的，请将其连接到一个光传感器，并使一个彩色传感器远离其他两个传感器。 屏幕传感器朝下 (在屏幕) 上时，其他传感器朝上朝上来测量环境光线。

![传感器 rig](images/sensor.png)

将 LED 灯面板连接到电源，并将其连接到 DAC。 微控制器必须能够控制发送到光源面板的电压，以便控制其强度，这是使用 DAC 实现的。 以下示意图显示了如何为我们使用的工具建立连接。 有关更多详细信息，请参阅传感器 PCB KiCad 项目。

![传感器示意图](images/SensorPCB.png)

### <a name="step-3---connect-the-microcontroller"></a>步骤 3-连接微控制器

将传感器连接到微控制器，并将微控制器连接到 PC。 出于我们的目的，我们将计算机控制测试与测试 (的系统) 。

下图显示了 MALT 的各个部分的连接方式。

![块示意图](images/BlockDiagram.png)

通过 MALT PCB，我们可以将 Arduino 板连接到传感器 PCB 和光源。 有关更多详细信息，请参阅 MALT PCB KiCad 项目。

![MALT 示意图](images/MaltPCB.png)

### <a name="step-4--start-testing"></a>步骤 4-开始测试

有关设置和使用刚刚组合的 MALT 的详细信息，请参阅 [测试系统亮度响应](testing-MALT-system-brightness-response.md) 。

#### <a name="test-scenarios-to-cover"></a>要涵盖的测试方案

* [测试自动亮度](testing-MALT-auto-brightness.md)

* [测试手动亮度](testing-MALT-manual-brightness.md)

* [测试系统方案](testing-MALT-system-scenarios.md)

请参考  
用于创建自定义测试的[微控制器命令](testing-MALT-microcontroller-commands.md)api。
