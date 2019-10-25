---
title: 邻近感应传感器阈值
description: 本主题提供有关邻近感应传感器阈值的信息。
ms.assetid: AD93421B-4787-4E56-B01D-58027EFEAC2D
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8efc03ba23371194e488235e2d5e74f08b0f81dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841763"
---
# <a name="proximity-sensor-thresholds"></a>邻近感应传感器阈值

没有为邻近感应传感器定义的可配置阈值。

邻近感应传感器驱动程序必须在 PKEY_SensorData_ProximityDetection 值发生更改时，通过调用[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready)来报告对传感器类扩展的示例读取。
邻近感应传感器驱动程序绝不应向类扩展报告第两行接近的读数，除非 PKEY_SensorData_ProximityDetection 已更改。

也就是说，近程传感器驱动程序必须始终在传感器类扩展调用[EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)回调之后报告一个示例读取。 此示例称为称为*初始示例读取*。

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)



