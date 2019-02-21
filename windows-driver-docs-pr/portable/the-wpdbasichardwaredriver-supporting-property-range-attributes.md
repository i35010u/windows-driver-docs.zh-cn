---
Description: Supporting the Property Range Attributes
title: 支持属性范围属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 692759b656b8e2cfd10c8a29910492772413b39c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525179"
---
# <a name="supporting-the-property-range-attributes"></a>支持属性范围属性


示例驱动程序支持两个属性： 更新间隔 (传感器\_更新\_间隔) 和当前的传感器读数 (传感器\_读取)。 每个属性支持一的组常规属性 （删除、 可读、 可写，等等）。 此外，这些属性支持特定范围属性 （最小值、 最大值和步长值）。

对于传感器读数，该属性表示为一个范围 (WPD\_属性\_特性\_窗体\_范围)。

属性属性分别对应于中的条目*Rs232connection.h*文件。 这些条目指定设备支持以及它在给定范围内的将属性设置时，可以使用应用程序的步骤值的最小值和最大值：

```cpp
#define SENSOR_READING_MIN 1  
#define SENSOR_READING_MAX 378  
#define SENSOR_READING_STEP 1   
```

设置这些范围特性的代码位于 WpdObjectProperties::GetPropertyAttributesForObject (在*Wpdobjectproperties.cpp*模块)。 此代码使用在中定义的值*Rs232connection.h*设置以下属性：

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





