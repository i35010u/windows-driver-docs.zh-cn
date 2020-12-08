---
title: 邻近感应传感器阈值
description: 本主题提供有关邻近感应传感器阈值的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f0be3437c7e4a7e47a2b362810f2e3c51b42920b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812265"
---
# <a name="proximity-sensor-thresholds"></a>邻近感应传感器阈值

没有为邻近感应传感器定义的可配置阈值。

邻近感应传感器驱动程序必须在 PKEY_SensorData_ProximityDetection 值发生更改时，通过调用 [SensorsCxSensorDataReady](/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready) 来报告对传感器类扩展的示例。
邻近感应传感器驱动程序绝不应向类扩展报告第两行接近的读数，除非 PKEY_SensorData_ProximityDetection 更改。

也就是说，近程传感器驱动程序必须始终在传感器类扩展调用 [EvtSensorStart](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config) 回调之后报告一个示例读取。 此示例称为称为 *初始示例读取*。

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)
