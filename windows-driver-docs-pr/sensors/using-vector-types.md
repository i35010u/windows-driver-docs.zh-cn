---
title: 使用与传感器的矢量类型
description: 使用与传感器的矢量类型
ms.assetid: cadc2cd3-10aa-4a4a-926f-edc01b046f27
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 621a63f0d81101bc8fca0fd9ddc0d3a4b685b42b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546479"
---
# <a name="using-vector-types-with-sensors"></a>使用与传感器的矢量类型


某些属性和数据字段包含的信息的数组。 例如，传感器\_属性\_LIGHT\_响应\_曲线属性包含 4 字节无符号整数的数组。 但是，当应用程序接收此类数组通过传感器 API，它们始终表示键入 VT\_向量 |UI1，单字节字符数组。

有关哪些属性和数据字段包含数组的信息，请参阅[常量](about-sensor-constants.md)。

下面的代码示例演示如何创建[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)对象，其中包含值为传感器\_属性\_LIGHT\_响应\_曲线。 名为 m 的变量\_pSensorProperties 是指向[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)接口。

```cpp
UINT responseCurve[10] = {0}; // Array to contain the response curve data.
// ****************************************************************************************
// The response curve consists of an array of byte pairs.
// The first byte contains the percentage brightness offset to be applied to the display.
// The second byte contains the corresponding ambient light value (in LUX).
// ****************************************************************************************
// (0, 10)
responseCurve[0] = 0; responseCurve[1] = 10;
// (10, 40)
responseCurve[2] = 10; responseCurve[3] = 40;
// (40, 80)
responseCurve[4] = 40; responseCurve[5] = 80;
// (68, 100)
responseCurve[6] = 68; responseCurve[7] = 100;
// (90, 150)
responseCurve[8] = 90; responseCurve[9] = 150;

// Create the buffer.
PROPVARIANT pvCurve = {0};
InitPropVariantFromBuffer(responseCurve, 10 * sizeof (UINT), &pvCurve);

// Add the values to the IPortableDeviceValues object.
hr = m_pSensorProperties->SetValue(SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE, &pvCurve);

PropVariantClear(&pvCurve);
```

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



