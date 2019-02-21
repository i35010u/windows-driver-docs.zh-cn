---
title: 创建通用驱动程序的永久唯一标识符基于传感器
description: 创建通用驱动程序的永久唯一标识符基于驱动程序
ms.assetid: B0131BC5-F76F-46B0-8BDE-4220D971AA29
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: dec58c2e7626c9848d221e60457ecf6a9bffb3a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541818"
---
# <a name="creating-a-persistent-unique-identifier-for-a-sensor"></a>创建一个传感器的永久唯一标识符


您的驱动程序必须创建*持久的唯一标识符*(PUID) 每个传感器。 PUID 是存储在会话之间并唯一地标识在设备上的对象的 GUID 值。 您的驱动程序必须返回 PUID 值查询的命名的属性时**DEVPKEY_Sensor_PersistentUniqueId**。 如果设备包含多个传感器，则必须自己 PUID 分配每个传感器。 应用程序可以使用检索此 ID [Windows.Devices.Enumeration](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration) WinRT Api。

您应创建新 PUID 为每个传感器，当传感器首次连接到计算机，，然后存储以供将来使用此值。

您的驱动程序应创建或检索之前调用 PUID [SensorsCxSensorInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensorinitialize)初始化例程。 此函数提供一个指向[SENSOR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_config)包含传感器配置的结构。 此指针可用于访问每个设备的特定属性存储。

## <a name="related-topics"></a>相关主题
[传感器驱动程序 ADXL345Acc 示例](https://go.microsoft.com/fwlink/p/?LinkId=617957)
<!--
https://go.microsoft.com/fwlink/p/?LinkId=617957: https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors/ADXL345Acc
-->
