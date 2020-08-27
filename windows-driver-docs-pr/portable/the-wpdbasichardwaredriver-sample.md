---
description: WpdBasicHardwareDriver 示例
title: WpdBasicHardwareDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f2274348fba76904d6fb6f6f30a7a8723f5f590
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969032"
---
# <a name="the-wpdbasichardwaredriver-sample"></a>WpdBasicHardwareDriver 示例


WpdBasicHardwareDriver 是支持九个设备的 WPD 驱动程序。 已选择这些设备，原因是它们十分简单。 这一简易性允许示例集中精力处理便携设备的常见任务，而无需陷入硬件复杂性。

此示例驱动程序基于也包含在 Windows 驱动程序工具包 (WDK) 中的 WpdHelloWorldDriver。 此驱动程序的 "支持 WPD 基础结构" 部分显示对 WpdHelloWorldDriver 源所做的更改，使其能够与基本硬件设备进行通信。 在完成文档的本部分中的主题之前，请先熟悉 WpdHelloWorldDriver。

如果打算开发与 Windows 8 集成传感器的驱动程序，请使用传感器 API 和驱动程序模型 (而不是 WPD) 。 如果开发驱动程序以便将传感器与 Windows Vista 或 Windows XP 集成，WPD 提供了一个可行的解决方案。

下表描述了 WpdBasicHardwareDriver 支持的传感器。

| 传感器                                         | 说明                                         |
|------------------------------------------------|-----------------------------------------------------|
| Memsic 2125 加速感应                      | 沿 X 轴和 Y 轴感应 +/-2g。          |
| Sensiron 温度和湿度传感器       | 感应温度和相对湿度。           |
| Flexiforce 传感器                              | 感应0-25 磅的压力。                      |
| PING Ultrasonic 传感器                         | 感应距离2-300 厘米。                     |
| 被动红外线 (PIR) 传感器                  | 感知运动。                                      |
| Hitachi HM55B 罗盘                          | 感应 (0-360 度) 。            |
| Hitachi H48C 三轴加速度            | 沿 X 轴、Y 轴和 Z 轴感应 +/-3g。 |
| Piezo 胶卷振动传感器 QTI (轻型) 传感器 | 感知振动。                                   |
| QTI (光源) 传感器                             | 感应光线强度。                             |

 

这九个传感器由加利福尼亚州 Rocklin 的 [视差公司](https://go.microsoft.com/fwlink/p/?linkid=154730) 销售。 可以单独购买，也可以一起购买传感器示例工具包。

若要将这些传感器与 WpdBasicHardwareDriver 配合使用，必须购买传感器、可编程的微控制器 (视差 BS2) 、测试板 (，例如视差基本戳记家庭板) 、RS232 电缆和其他部件。 所有此硬件都可从视差获取，并可通过其网站进行排序。

线路设计基于其传感器数据表中视差提供的示例线路。 这些线路旨在将每个传感器与视差 BS2 可编程微控制器集成。

每个九个线路中的微控制器固件都包含在 \\ \\ \\ Windows 驱动程序工具包 (WDK) 的 src wpd WpdBasicHardwareDriver 固件子目录中。

 

 




