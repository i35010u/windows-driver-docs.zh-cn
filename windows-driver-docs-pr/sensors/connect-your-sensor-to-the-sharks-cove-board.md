---
title: 将传感器连接到带 Cove 板
description: 本主题提供有关如何将传感器测试板连接到带 Cove 板的指导。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e8ebeba4e37f7761460a687f4c9de9f8c37a8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831067"
---
# <a name="connect-your-sensor-to-the-sharks-cove-board"></a>将传感器连接到带 Cove 板


本主题提供有关如何将传感器测试板连接到带 Cove 板的指导。

在 ADXL345 加速感应方案中，进行任何必要的修改后，最终会将测试板连接到带 Cove，如下图所示。

![带 cove 和 adxl345 加速感应板的连接关系图。](images/sensor-header.png)

若要在传感器分类板与带 Cove 之间实现稳定可靠的连接，可以先焊接将8针单行男标头到专题讨论板上，如下图所示。

![adxl345 加速度分布板的图像，其中显示8针，单行男标头。](images/adxl-header.png)

然后，使用8个女性到女性跳线的功能区 (如下所示) ，根据前面的连接关系图将传感器的带 Cove 连接到该。

![adxl345 传感器 brrakout 板和8线接线器电线集。](images/snsr-n-jumpers.png)

下面是有关 ADXL345 数据表中信息和带 Cove 技术规范 Rev 1.0 的一些示例，帮助我们到达上图中所示的连接策略：

**J1C1 PIN4** 连接到加速感应板上的 **VDD** 和 **CS** 。

-   **VDD** 是数字接口的供应电压线。 我们决定在采用双电压配置的情况下使用加速感应，同时保持功耗低。 那么，在四个可用电压 (**J1C1 PIN1-PIN4**) 我们的目标是这两个最低电压。 **J1C1 PIN4** 上的 **J1C1 PIN3** 和 1.8 v 上都是 2.8 v。 在双电压配置中， **VDD** 必须连接到低于 **VS** 的电压。 我们已将 **VDD** 连接到 **J1C1 PIN4**，带 Cove 上的 1.8 v 线。
-   **CS** 是用于加速感应的通信模式选择 pin。 若要启用 I2C 通信模式，必须将 **CS** 高，在本例中为 **VDD**，这是在 [准备传感器测试板](prepare-your-sensor-test-board.md)中使用蓝线进行修改时处理的。 修改会将 **VDD** 和 **CS** 从加速感应板与 **J1C1 PIN4**（1.8 v 线）结合在一起。

**J1C1 PIN12** 连接到加速板上的 **SDO** 。

-   当 **SDO** 行较高时，加速感应板的7位 I2C 地址是0x1D，后跟 R/W 位。 当 **SDO** 行 (（即连接到地面) ）时，加速感应板的 I2C 地址为0x53，后跟 R/W 位。 在 Microsoft SPBAccelerometer 示例中，决定使用0x53 的地址。 这就是在带 Cove 上， **SDO** 行连接到地面 (**J1C1 PIN12**) 的原因。

前面的项目符号中所述的连接决定基于 " *操作理论* " 部分中的信息， (第6页) 和 ADXL345 数据表 (第) 8 页的 *串行通信* 部分。

成功将传感器测试板连接到带 Cove 后，请阅读下一主题，了解有关如何 [编写和部署通用传感器驱动程序](write-and-deploy-your-universal-sensor-driver.md)的指南。

 

 




