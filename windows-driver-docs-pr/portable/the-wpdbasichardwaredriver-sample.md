---
Description: The WpdBasicHardwareDriver Sample
title: WpdBasicHardwareDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d01f448d5fd25800c1c37c15eab1f17f3c976f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519591"
---
# <a name="the-wpdbasichardwaredriver-sample"></a>WpdBasicHardwareDriver 示例


WpdBasicHardwareDriver 是支持九个设备一个 WPD 驱动程序。 由于其简单性选择这些设备。 这种简单性允许示例可以专注于任务所共有的便携设备而无需获取硬件复杂性中而不能自拔。

此示例驱动程序基于 WpdHelloWorldDriver 也包括 Windows Driver Kit (WDK) 中。 此驱动程序的"支持 WPD 基础结构"部分显示，以便它可以与基本硬件设备通信对 WpdHelloWorldDriver 源所做的更改。 通过文档的此部分中的主题工作之前，先熟悉 WpdHelloWorldDriver。

如果你打算开发将传感器与 Windows 8 集成的驱动程序，使用传感器 API 和驱动程序模型 （而非 WPD）。 如果开发驱动程序，以将传感器与 Windows Vista 或 Windows XP 相集成，WPD 提供可行的解决方案。

下表所述 WpdBasicHardwareDriver 支持传感器。

| Sensor                                         | 描述                                         |
|------------------------------------------------|-----------------------------------------------------|
| Memsic 2125 加速感应器                      | + /-2g 沿 x 轴和 y 轴的意义。          |
| Sensiron 温度和湿度传感器       | 检测到温度和湿度相对。           |
| Flexiforce 传感器                              | 从 0-25 lbs 的感官压力。                      |
| PING Ultrasonic 传感器                         | 检测到 2-300 cm 之间的距离。                     |
| 被动红外 (PIR) 传感器                  | 感官运动。                                      |
| 人： Hitachi HM55B 指南针                          | 检测到磁场方位 (0-360 度为单位)。            |
| 人： Hitachi H48C 三轴加速感应器            | + /-3g 沿 x 轴、 y 轴和 z 轴的意义。 |
| Piezo 电影振动传感器 QTI （轻型） 传感器 | 检测到振动。                                   |
| QTI （轻型） 传感器                             | 感官浅色强度。                             |

 

这九个传感器由销售[视差 Corporation](https://go.microsoft.com/fwlink/p/?linkid=154730) Rocklin，加利福尼亚州。 它们可购买单独或一起的传感器示例工具包。

若要使用 WpdBasicHardwareDriver 这些传感器，必须购买传感器、 可编程微控制器 (视差 BS2)、 （如视差 BASIC 戳家庭作业看板中） 的测试板、 RS232 电缆和其他部分。 这个硬件的所有可从视差，并且可以通过其网站进行排序。

线路设计基于在其传感器数据工作表中提供的示例线路。 这些线路设计为与视差 BS2 可编程微控制器的每个传感器。

为每个九个线路的微型控制器固件包含在 src\\wpd\\WpdBasicHardwareDriver\\固件子目录 Windows Driver Kit (WDK) 中。

 

 




