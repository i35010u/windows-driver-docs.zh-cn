---
title: 为基于通用驱动程序的传感器创建持久的唯一标识符
description: 为基于通用驱动程序的驱动程序创建持久的唯一标识符
ms.assetid: B0131BC5-F76F-46B0-8BDE-4220D971AA29
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2b5cde5f629ad93b38c794dd324da9dcfe050196
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837626"
---
# <a name="creating-a-persistent-unique-identifier-for-a-sensor"></a>为传感器创建持久的唯一标识符


驱动程序必须为每个传感器创建一个*持久的唯一标识符*（PUID）。 PUID 是跨会话存储并在设备上唯一标识该对象的 GUID 值。 在查询名为**DEVPKEY_Sensor_PersistentUniqueId**的属性时，驱动程序必须返回 PUID 值。 如果设备包含多个传感器，则必须为每个传感器分配其自己的 PUID。 应用程序可以使用[Windows.](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration) Can WinRT api 检索此 ID。

当传感器第一次连接到计算机时，应该为每个传感器创建新的 PUID，并存储此值供以后使用。

在调用[SensorsCxSensorInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensorinitialize)初始化例程之前，驱动程序应创建或检索 PUID。 此函数提供一个指向[SENSOR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_config)结构的指针，该结构包含传感器配置。 此指针可用于访问每个设备的特定属性存储。

## <a name="related-topics"></a>相关主题
[传感器驱动程序 ADXL345Acc 示例](https://go.microsoft.com/fwlink/p/?LinkId=617957)
<!--
https://go.microsoft.com/fwlink/p/?LinkId=617957: https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors/ADXL345Acc
-->
