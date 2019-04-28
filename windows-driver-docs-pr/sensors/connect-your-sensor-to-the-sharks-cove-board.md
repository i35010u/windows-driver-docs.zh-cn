---
title: 将传感器连接到 Shark Cove 板
description: 本主题提供有关如何将传感器测试开发板连接到 Shark Cove 板指南。
ms.assetid: B081F4B6-D15E-4F1A-A5C0-E19DA806EAB2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4ecd4204e2841db1d5825018d30b8ba4d2cf633
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338374"
---
# <a name="connect-your-sensor-to-the-sharks-cove-board"></a>将传感器连接到 Shark Cove 板


本主题提供有关如何将传感器测试开发板连接到 Shark Cove 板指南。

在 ADXL345 加速感应器方案中，并进行任何必要的修改后，结果会导致连接到 Shark Cove，如以下关系图中所示的加速感应器测试板起作用。

![shark cove 和 adxl345 加速感应器面板的连接关系图。](images/sensor-header.png)

若要实现传感器专题板和 Shark Cove 之间稳定、 可靠的连接，无法启动的焊接 8 pin 的单行男性标头到多个专题板中，在下图中所示。

![adxl345 加速感应器专题看板，显示 8 pin、 单行男性标头的图像。](images/adxl-header.png)

然后使用功能区的八个女性女性跳线 （如下所示），将传感器专题开发板连接到 Shark Cove，根据上图中连接。

![adxl345 传感器 brrakout 板和跳线 8 在线女性女性集。](images/snsr-n-jumpers.png)

下面是一些示例如何 ADXL345 数据工作表和 Shark Cove 技术规范修订版 1.0 中的信息帮助我们到达在上图中所示的连接策略：

**J1C1 PIN4**连接到**VDD**并**CS**加速感应器板上。

-   **VDD**供电电压线为数字的接口。 我们决定在双电压配置中，使用加速感应器，还保持较低的功率消耗。 因此，带四个可用的电压 (**J1C1 PIN1-PIN4**) 我们针对两个最低的。 这些选项位于 2.8V **J1C1 PIN3**和 1.8 上的 v **J1C1 PIN4**。 在双电压配置中， **VDD**必须连接到比低电压**VS**。 因此我们已连接**VDD**到**J1C1 PIN4**、 1.8 v 行 Shark Cove 上。
-   **CS**是加速感应器的通信模式选择 pin。 若要启用 I2C 通信模式，您必须将**CS**高，在本例中为**VDD**，这是由负责使用蓝色在线修改[准备在传感器测试板](prepare-your-sensor-test-board.md). 修改将联系两者**VDD**并**CS**到板的加速感应器**J1C1 PIN4**、 1.8 v 行。

**J1C1 PIN12**连接到**SDO**加速感应器板上。

-   当**SDO**行量较高，加速感应器板的 7 位 I2C 地址 0x1D 后, 跟的读/写位。 当**SDO**行较低 （即连接到接地）、 加速感应器板的 I2C 地址是 0x53 后, 跟的读/写位。 在 Microsoft SPBAccelerometer 示例中，因此决定将使用 0x53 的地址。 而这正是**SDO**线路连接到接地引脚 (**J1C1 PIN12**) Shark Cove 上。

中的信息通过前面的项目符号中所述的连接决策*操作从理论上讲*部分 （第 6 页） 和*串行通信*ADXL345 数据部分 （第 8 页）工作表。

有关详细 Shark Cove 板有关技术信息，请参阅[Shark Cove 示意](https://firmware.intel.com/sites/default/files/Sharks_Cove_Schematic.pdf)。

已成功连接后在传感器测试板到 Shark Cove，读取下一主题以获取有关如何指导[编写和部署通用传感器驱动程序](write-and-deploy-your-universal-sensor-driver.md)。

 

 




