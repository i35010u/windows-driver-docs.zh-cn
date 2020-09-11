---
title: 为基于通用驱动程序的传感器创建持久的唯一标识符
description: 为基于通用驱动程序的驱动程序创建持久的唯一标识符
ms.assetid: B0131BC5-F76F-46B0-8BDE-4220D971AA29
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 86ad391c3c6801fc45f98781270927e976861618
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010113"
---
# <a name="creating-a-persistent-unique-identifier-for-a-sensor"></a>为传感器创建持久的唯一标识符


驱动程序必须为每个传感器 (PUID) 创建 *永久唯一标识符* 。 PUID 是跨会话存储并在设备上唯一标识该对象的 GUID 值。 查询名为 **DEVPKEY_Sensor_PersistentUniqueId**的属性时，驱动程序必须返回 PUID 值。 如果设备包含多个传感器，则必须为每个传感器分配其自己的 PUID。 应用程序可以使用 [Windows.](/uwp/api/Windows.Devices.Enumeration) Can WinRT api 检索此 ID。

当传感器第一次连接到计算机时，应该为每个传感器创建新的 PUID，并存储此值供以后使用。

在调用 [SensorsCxSensorInitialize](/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensorinitialize) 初始化例程之前，驱动程序应创建或检索 PUID。 此函数提供一个指针，指向包含传感器配置的 [SENSOR_CONFIG](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_config) 结构。 此指针可用于访问每个设备的特定属性存储。

## <a name="related-topics"></a>相关主题
[传感器驱动程序 ADXL345Acc 示例](https://go.microsoft.com/fwlink/p/?LinkId=617957)
<!--
https://go.microsoft.com/fwlink/p/?LinkId=617957: https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors/ADXL345Acc
-->