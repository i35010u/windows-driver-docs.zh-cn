---
title: 支持多个传感器
description: SpbAccelerometer 示例演示如何编写一个传感器设备的驱动程序。
ms.assetid: 633B7CB5-EF4A-42BE-A60E-7D12BDAFA34F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05876f4790b01a2589c92e1bafab2809b599ad7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575857"
---
# <a name="supporting-multiple-sensors"></a>支持多个传感器


SpbAccelerometer 示例演示如何编写一个传感器设备的驱动程序。 但是，传感器类扩展和传感器 ddi 的可以容纳多个传感器设备。 请考虑以下修改以支持多个传感器的示例驱动程序。

SensorDdi 分为两个类：

1.  SensorDdi
2.  Sensor

SensorDdi 类将继续通过实现来促进与传感器类扩展的通信**ISensorDriver**接口，并通过调用**ISensorClassExtension**接口。 此类还应该维护电流传感器，传感器 ID 字符串按索引的列表。

对于每个传感器，创建新的传感器类实例。 此类将维护： 状态、 属性和数据字段。 每个传感器示例也将具有其自己的 ClientManager 和 ReportManager。

在接收时一个传感器 DDI 回调，SensorDDI 类将与传感器 ID 匹配，并调用相应的传感器实例中的相应方法。

左侧和右侧的下图描绘了在下载时存在的示例驱动程序。 右侧的图描绘了此驱动程序之后应用了本主题中的修改并添加了对另一台设备支持。

![多个传感器支持](images/multi-sensor.png)

 

 




