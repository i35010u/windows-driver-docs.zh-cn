---
title: 光传感器属性
description: 光线传感器属性键。
ms.assetid: 87C58F14-E23D-4567-BBD5-AA42DF9371B0
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 57161a83aa5e8690f2861fffc3940622d93c44cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569323"
---
# <a name="light-sensor-property"></a>光传感器属性


光线传感器属性键。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>属性键</th>
<th>在任务栏的搜索框中键入</th>
<th>访问 （R/O，R/W）</th>
<th>必需/可选</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_LightSensor_ResponseCurve</p></td>
<td><p>VT_VECTOR | VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必需</p></td>
<td><p>响应光线传感器的曲线。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_SensorData_LightLevel_AutoBrightnessPreferred</p></td>
<td><p>VT_BOOL</p></td>
<td><p>R/O</p></td>
<td><p>可选</p></td>
<td><p>光线传感器是自动亮度的首选。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_SensorData_LightLevel_ColorCapable</p></td>
<td><p>VT_BOOL</p></td>
<td><p>R/O</p></td>
<td><p>可选。 如果支持色度和浅温度，必需。</p></td>
<td><p>光线传感器支持浅色温度和/或色度 x / y。</p></td>
</tr>
</tbody>
</table>

 

有关数据类型的详细信息中所示**类型**列中，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

**注释**

若要使用此属性键来设置其相关属性的值，可以使用**InitPropVariantFromUInt32Vector**函数。 例如，若要将值设置为传感器\_属性\_最小值\_数据\_间隔属性使用主键\_传感器\_MinimumDataInterval\_Ms 属性键，使用以下语法：

```cpp
// Sensor Properties
     if (NT_SUCCESS(Status))
     {
         Status = InitSensorCollection(SENSOR_PROPERTIES_COUNT, &amp;m_pSensorProperties, SensorInstance);
         if (NT_SUCCESS(Status))
         {
               m_Interval = DEFAULT_ACCELEROMETER_REPORT_INTERVAL;
               ...
               ...
               m_pSensorProperties->List[SENSOR_PROPERTY_MIN_DATA_INTERVAL].Key = PKEY_Sensor_MinimumDataInterval_Ms;
               InitPropVariantFromUInt32(ACCELEROMETER_MIN_REPORT_INTERVAL, &amp;(m_pSensorProperties->List[SENSOR_PROPERTY_MIN_DATA_INTERVAL].Value));
               ...
         }
    }
```

要设置通过使用其相关的属性键的传感器属性的完整示例，请参阅[client.cpp 文件](https://github.com/Microsoft/Windows-driver-samples/blob/master/sensors/ADXL345Acc/client.cpp)ADXL345Acc 示例驱动程序，和向下的滚动到**NTSTATUS ADXL345AccDevice::Initialize （...)** 例程。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


**标头：** Sensorsdef.h

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[其他传感器属性](other-sensor-properties.md)

 

 






