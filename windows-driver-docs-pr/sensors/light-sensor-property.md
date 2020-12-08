---
title: 光传感器属性
description: 光源传感器的属性键。
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 227b751a84c2c7eb39a06ba22f9cec0d9743d981
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812317"
---
# <a name="light-sensor-property"></a>光传感器属性

光源传感器的属性键。

| 属性键 | 类型 | Access (R/O，R/W)  | 必需/可选 | 说明 |
| --- | --- | --- | --- | --- |
| PKEY_LightSensor_ResponseCurve | VT_VECTOR | R/O | 必须 | 光传感器的响应曲线。 |
| DEVPKEY_SensorData_LightLevel_AutoBrightnessPreferred | VT_BOOL | R/O | 可选 | 光源传感器是自动亮度的首选。 |
| DEVPKEY_SensorData_LightLevel_ColorCapable | VT_BOOL | R/O | 可选 | 如果支持 chromaticity 和轻型温度，则是必需的。 光源传感器支持轻型温度和/或 chromaticity x/y。 |

有关 " **类型** " 列中显示的数据类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

## <a name="remarks"></a>备注

若要使用此属性键设置其相关属性的值，可以使用 **InitPropVariantFromUInt32Vector** 函数。 例如，若要 \_ \_ \_ 使用 PKEY 传感器 MinimumDataInterval Ms 属性键设置 "传感器属性最小数据间隔" 属性的值 \_ \_ \_ \_ ，请使用以下语法：

```cpp
// Sensor Properties
     if (NT_SUCCESS(Status))
     {
         Status = InitSensorCollection(SENSOR_PROPERTIES_COUNT, &m_pSensorProperties, SensorInstance);
         if (NT_SUCCESS(Status))
         {
               m_Interval = DEFAULT_ACCELEROMETER_REPORT_INTERVAL;
               ...
               ...
               m_pSensorProperties->List[SENSOR_PROPERTY_MIN_DATA_INTERVAL].Key = PKEY_Sensor_MinimumDataInterval_Ms;
               InitPropVariantFromUInt32(ACCELEROMETER_MIN_REPORT_INTERVAL, &(m_pSensorProperties->List[SENSOR_PROPERTY_MIN_DATA_INTERVAL].Value));
               ...
         }
    }
```

有关使用其相关的属性键设置传感器属性的完整示例，请参阅 ADXL345Acc 示例驱动程序中的 [客户端 .cpp 文件](https://github.com/Microsoft/Windows-driver-samples/blob/master/sensors/ADXL345Acc/client.cpp) ，并向下滚动到 **NTSTATUS ADXL345AccDevice：： Initialize ( ... )** 例程。

**标头：** Sensorsdef
