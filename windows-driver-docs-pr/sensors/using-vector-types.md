---
title: 使用带有传感器的矢量类型
description: 使用带有传感器的矢量类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe16f5c69a5e12c879c03a51aca26353aba0c430
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812093"
---
# <a name="using-vector-types-with-sensors"></a>使用带有传感器的矢量类型


某些属性和数据字段包含信息的数组。 例如，"传感器 \_ 属性 \_ 灯 \_ 响应曲线" \_ 属性包含4字节无符号整数的数组。 但是，当应用程序通过传感器 API 接收此类数组时，它们始终表示为类型 VT \_ VECTOR |UI1，单字节字符数组。

有关哪些属性和数据字段包含数组的信息，请参阅 [常量](about-sensor-constants.md)。

下面的代码示例演示如何创建一个 [IPortableDeviceValues](/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues) 对象，该对象包含传感器 \_ 属性 \_ 光源 \_ 响应 \_ 曲线的值。 名为 m pSensorProperties 的变量 \_ 是指向 [IPortableDeviceValues](/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues) 接口的指针。

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
[传感器地理位置驱动程序示例](../gnss/sensors-geolocation-driver-sample.md)
