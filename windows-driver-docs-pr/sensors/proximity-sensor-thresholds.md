---
title: 邻近感应传感器阈值
description: 本主题提供有关邻近感应传感器阈值的信息。
ms.assetid: AD93421B-4787-4E56-B01D-58027EFEAC2D
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2b32ec8cfb3c43c9389c312ea6176d9e0255b4ac
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010639"
---
# <a name="proximity-sensor-thresholds"></a>邻近感应传感器阈值

没有为邻近感应传感器定义的可配置阈值。

邻近感应传感器驱动程序必须在 PKEY_SensorData_ProximityDetection 值发生更改时，通过调用 [SensorsCxSensorDataReady](/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready) 来报告对传感器类扩展的示例。
邻近感应传感器驱动程序绝不应向类扩展报告第两行接近的读数，除非 PKEY_SensorData_ProximityDetection 更改。

也就是说，近程传感器驱动程序必须始终在传感器类扩展调用 [EvtSensorStart](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config) 回调之后报告一个示例读取。 此示例称为称为 *初始示例读取*。

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)