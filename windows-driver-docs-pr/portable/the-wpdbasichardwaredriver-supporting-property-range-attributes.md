---
description: 支持属性范围特性
title: 支持属性范围特性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29d798880d0e1d898861b60bbce7a5f4b630686b
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969168"
---
# <a name="supporting-the-property-range-attributes"></a>支持属性范围特性


示例驱动程序支持两个属性：更新间隔 (传感器 \_ 更新 \_ 间隔) 和当前传感器读数 (传感器 \_ 读数) 。 其中每个属性都支持 (删除、可读、可写等) 的一组常规属性。 此外，这些属性还支持)  (最小值、最大值和步长值的特定范围属性。

对于传感器读数，属性表示为范围 (WPD \_ 属性 \_ 属性 \_ 窗体 \_ 范围) 。

属性特性对应于 *rs232connection.cpp* 文件中的项。 这些条目指定设备支持的最小值和最大值，以及应用程序在给定范围内设置属性时可以使用的步长值：

```cpp
#define SENSOR_READING_MIN 1  
#define SENSOR_READING_MAX 378  
#define SENSOR_READING_STEP 1   
```

可在 *WpdObjectProperties* 模块) 中的 WpdObjectProperties：： GetPropertyAttributesForObject (中找到设置这些范围属性的代码。 此代码使用 *rs232connection.cpp* 中定义的值来设置以下属性：

```cpp
else if (IsEqualPropertyKey(Key, SENSOR_READING))
{
    // Form range attributes for the temperature reading property
    hr = pAttributes->SetUnsignedIntegerValue(WPD_PROPERTY_ATTRIBUTE_FORM, 
                                              WPD_PROPERTY_ATTRIBUTE_FORM_RANGE);
    CHECK_HR(hr, 
             "Failed to set WPD_PROPERTY_ATTRIBUTE_RANGE_MIN 
              for SENSOR_READING");

    hr = pAttributes->SetUnsignedIntegerValue(WPD_PROPERTY_ATTRIBUTE_RANGE_MIN, 
                                              SENSOR_READING_MIN);
    CHECK_HR(hr, 
             "Failed to set WPD_PROPERTY_ATTRIBUTE_RANGE_MIN 
              for SENSOR_READING");

    hr = pAttributes->SetUnsignedIntegerValue(WPD_PROPERTY_ATTRIBUTE_RANGE_MAX, 
                                              SENSOR_READING_MAX);
    CHECK_HR(hr, 
             "Failed to set WPD_PROPERTY_ATTRIBUTE_RANGE_MAX 
              for SENSOR_READING");

    hr = pAttributes->SetUnsignedIntegerValue(WPD_PROPERTY_ATTRIBUTE_RANGE_STEP, 
                                              SENSOR_READING_STEP);
    CHECK_HR(hr, 
             "Failed to set WPD_PROPERTY_ATTRIBUTE_RANGE_STEP 
              for TEMPERATURE_SENSOR_READING");
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





