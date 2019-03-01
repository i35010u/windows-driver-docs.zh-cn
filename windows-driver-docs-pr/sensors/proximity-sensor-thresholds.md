---
title: 邻近传感器阈值
description: 本主题提供有关邻近信息传感器的阈值。
ms.assetid: AD93421B-4787-4E56-B01D-58027EFEAC2D
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7c74b23e558e490338b82963f6b06abc7e5e29b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547244"
---
# <a name="proximity-sensor-thresholds"></a>邻近传感器阈值

为接近传感器定义没有可配置的阈值。

邻近传感器驱动程序必须报告的示例通过调用读取至传感器类扩展[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)每当 PKEY_SensorData_ProximityDetection 值发生更改。
除非 PKEY_SensorData_ProximityDetection 发生更改，邻近传感器驱动程序应永远不会报告行两个邻近读取至类扩展中。

话虽如此，邻近传感器驱动程序必须始终报告一个示例读取传感器类扩展调用后立即[EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)回调。 此示例称为嘿 *初始示例读取*。

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)



