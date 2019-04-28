---
title: 准备在传感器测试板
description: 本主题演示如何为连接到 Shark Cove 板准备传感器测试开发板。
ms.assetid: 121A6B05-9D5D-447C-B7C6-B2B86C24114B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cd9a3ee3371170d2afe5ba620096d3f1a69c935
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330132"
---
# <a name="prepare-your-sensor-test-board"></a>准备在传感器测试板


本主题演示如何为连接到 Shark Cove 板准备传感器测试开发板。

**请注意**  本主题假定你使用的传感器测试板 (有时称为传感器*专题*板) 从 IHV，购买的和不开发传感器测试板专用于与 Shark Cove 一起使用。

 

如果从 IHV 购买传感器测试开发板，并且它不开发的专用于 Shark Cove，可能需要对测试板进行一些修改。 本主题说明必须阅读以了解你是否需要修改您的传感器测试板的信息的类型。 如果需要修改传感器测试板，然后按照本主题为连接到 Shark Cove 准备测试板中的指南。

选择要为其生成通用传感器驱动程序的传感器后，便必须获得传感器，制造商的数据表和 Shark Cove 的技术规格。

Shark Cove 板还提供了不同的标头以允许连接到外部设备。 20 pin 男性标头，标记为 J1C1 传感器标头，可以将传感器连接到 Shark Cove。 传感器连接到 J1C1，与 Shark Cove 使用 I2C 简单外围总线 （存储） 进行通信。

研究的数据表和技术规范，以找出如何将您连接到 J1C1 的传感器测试板球瓶 （或其他连接点）。

以下是从表*Shark Cove 技术规范修订版 1.0*，显示 J1C1 的 pin 分配。

| J1C1 pin\# | 信号名称            | 备注                                                                                            |
|------------|------------------------|-----------------------------------------------------------------------------------------------------|
| 1          | +V3P3A\_PLT            | 3.3V 电源导轨                                                                                     |
| 2          | + VSYS (4.2)            | 4.2 V 电源线                                                                                    |
| 3          | +V2P8\_ALDO1           | 2.8V 模拟电源线                                                                              |
| 4          | +V1P8A                 | 1.8 V 电源线                                                                                    |
| 5          | 地面                 | 地线                                                                                              |
| 6          | 地面                 | 地线                                                                                              |
| 7          | ACCEL\_INT\_N          | 加速感应器中断信号                                                                      |
| 8          | HDR\_GYRO\_INT1        | 陀螺仪中断信号                                                                          |
| 9          | HDR\_指南针\_DRDY     | 准备就绪信号                                                                                        |
| 10         | HDR\_GYRO\_INT2        | 陀螺仪中断信号                                                                          |
| 11         | 地面                 | 地线                                                                                              |
| 12         | 地面                 | 地线                                                                                              |
| 13         | HDR\_I2C\_2\_SDA       | I2C 控制器 2 的 I2C 数据行                                                                  |
| 14         | HDR\_PROX\_ALS\_INT\_N | 环境光线传感器中断信号                                                               |
| 15         | HDR\_I2C\_2\_SCL       | I2C 时钟行 I2C 控制器 2                                                                 |
| 16         | SAR\_PROX\_INT         | 如果此信号需要用于特别行政区\_PROX\_INT，它必须配置为中断信号\*。 |
| 17         | 未连接          | 无                                                                                                |
| 18         | SAR\_PROX\_RST         | 邻近传感器重置信号                                                                       |
| 19         | 未连接          | 无                                                                                                |
| 20         | 未连接          | 无                                                                                                |

 

有关详细 Shark Cove 板有关技术信息，请参阅[Shark Cove 示意](https://firmware.intel.com/sites/default/files/Sharks_Cove_Schematic.pdf)。

如果，例如，您必须选择生成 ADXL345 加速感应器通用传感器驱动程序，然后从页面 5 ADXL345 数字加速感应器数据工作表 （以及在同一页上的表 4) 的以下关系图显示可用于连接插针到 Shark Cove 加速感应器看板。

![adxl345 加速感应器管脚配置。](images/adxl345-pins.png)

此加速感应器是可从[SparkFun](https://www.sparkfun.com/products/9836)、 已与以下示意图专题看板上装载。

![无需修改即可 adxl345 专题看板的关系图。](images/adxl-breakout.png)

请注意，在关系图中，确认 VDD/IO 行 （引脚 1） 已连接到 VS 行 （引脚 6）。 并请注意，此外，不直接向 8 pin 标头公开 VDD/IO 行。

但是，在 ADXL345 数据表 19 页中，建议 VDD/IO 和 VS 应连接到不同的供应电压行，以减少与行上的数字时钟干扰。 数据表的第 10 页上所示，我们必须将绑定从高到 VDD/IO，若要选择的 I2C 通信模式的 CS 行。

因此下, 图显示对 ADXL345 专题板，使其可使用示例传感器驱动程序必须进行的修改。

![修改后的 adxl345 加速感应器专题看板的关系图。](images/adxl-breakout-mod.png)

换而言之，按如下所示修改 ADXL345 专题板：

-   剪切到 VS 行连接 VDD/IO 行跟踪。 然后检查通过测量 pin 1 和万用表，以确保可以打开线路的 pin 6 之间。
-   焊接以有线方式连接到 CS 行 （引脚 7） 的 VDD/IO 行。 然后万用表，以确保具有 pin 1 和 pin 7 之间的短路的度量值。

下面是显示修改后的 ADXL345 加速感应器专题板的图像。

![已修改的 adxl345 加速感应器专题看板的实际的图像。](images/adxl-mod-real.png)

已添加到上图中，并在 ADXL345 芯片以指示 pin 1 的位置上放置一个黄点。

因此准备传感器测试开发板连接到 Shark Cove 可能涉及的以下任意或全部：

-   剪切中断传感器测试板上的组件之间的不需要的连接的印刷电路板 (pcb) 轨道。
-   剪切 PCB 跟踪和重新连接路由到传感器上的新目标测试板。
-   焊接到传感器测试板女性，因此使得能够位移连接器 (IDC) 标头的功能区电缆。 这样就简单且方便地连接两个板。
-   作为上述项目符号的替代方法，可以找到一种方法，将传感器测试板装载电路试验板，然后查找 J1C1 的匹配针脚连接电路试验板的相关行的简便方法。

所做的所有必要的修改到传感器测试板后，请按照下一主题中的指导[传感器连接到 Shark Cove 板](connect-your-sensor-to-the-sharks-cove-board.md)。

 

 




