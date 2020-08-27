---
description: 定义传感器对象
title: 定义传感器对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 509fe6f58f69abc26c0b68c6416a6ef3e853fb00
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969182"
---
# <a name="defining-the-sensor-objects"></a>定义传感器对象


在 (WPD) 的 Windows 便携设备中，设备上的逻辑实体称为对象。 对象可以表示设备的信息性部分或功能部分。 任何对象都具有一个或多个属性。 可以将属性视为对象描述元数据。 例如，样本温度和湿度传感器上的 TempHumidity 对象支持传感器 \_ 读取属性。 此属性指定设备获得的当前温度和相对湿度。

WpdHelloWorldDriver 支持下表中显示的对象。

| 对象  | 说明                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| 设备  | 包含描述性属性的根对象，例如固件版本、型号和友好名称。 |
| 存储 | 公开属性的对象，例如存储容量、文件系统类型和可用字节数。         |
| 文件夹  | 公开属性的对象，例如文件夹名称。                                                             |
| 文件    | 公开属性的对象，例如文件名和实际文件内容。                                      |

 

由于示例传感器不支持存储、文件夹或文件对象，因此 WpdBasicHardwareDriver 不实现这些对象。 相反，每个传感器类型都由单个对象表示。 下表列出了 WpdBasicHardwareDriver 支持的对象。

| 对象       | 说明                                                                                                                                |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| 设备       | 包含描述性属性的根对象，例如固件版本、型号和友好名称。                 |
| TempHumidity | 用于显示温度读数和湿度读数以及可编辑的更新间隔属性的功能对象。 |
| 指南针      | 用于显示罗盘读数的功能对象，以及可以编辑的更新间隔属性。                          |
| PIR          | 此功能对象显示被动红外读取，以及可以编辑的更新间隔属性。                 |
| QTI          | 一个功能对象，它显示环境光线读数，以及一个可以编辑的更新间隔属性。                    |
| Flex         | 用于显示压力读数的函数对象以及可以编辑的更新间隔属性。                         |
| Ping         | 一个函数对象，该对象显示读取距离，以及可以编辑的更新间隔属性。                         |
| Piezo        | 用于显示振动读数以及可编辑的更新间隔属性的功能对象。                        |
| Memsic       | 用于显示2轴加速度感应读取的功能对象，以及可以编辑的更新间隔属性。             |
| 架式      | 一个可显示3轴加速度感应的功能对象，以及一个可以编辑的更新间隔属性。             |

 

在 WPD 中，对象由字符串标识。 设备对象的字符串标识符是在 *Portabledevice* 文件中定义的：

```cpp
#define WPD_DEVICE_OBJECT_ID  L"DEVICE"
```

传感器对象的字符串标识符在 WpdBasicHardwareDriver 的 *WpdObjectProperties* 文件中定义：

```cpp
#define SENSOR_OBJECT_ID             L"Sensor"
#define SENSOR_OBJECT_NAME_VALUE          L"Parallax Sensor"
#define COMPASS_SENSOR_OBJECT_ID              L"Compass"
#define COMPASS_SENSOR_OBJECT_NAME_VALUE      L"HM55B Compass Sensor"
#define PIR_SENSOR_OBJECT_ID                  L"PIR"
#define PIR_SENSOR_OBJECT_NAME_VALUE          L"Passive Infra-Red Sensor"
#define QTI_SENSOR_OBJECT_ID                  L"QTI"
#define QTI_SENSOR_OBJECT_NAME_VALUE          L"QTI Light Sensor"
#define FLEX_SENSOR_OBJECT_ID                 L"Flex"
#define FLEX_SENSOR_OBJECT_NAME_VALUE         L"Flex Force Sensor"
#define PING_SENSOR_OBJECT_ID                 L"Ping"
#define PING_SENSOR_OBJECT_NAME_VALUE         L"Ultrasonic Distance Sensor"
#define PIEZO_SENSOR_OBJECT_ID                L"Piezo"
#define PIEZO_SENSOR_OBJECT_NAME_VALUE        L"Piezo Vibration Sensor"
#define TEMP_SENSOR_OBJECT_ID                 L"TempHumidity"
#define TEMP_SENSOR_OBJECT_NAME_VALUE         L"Sensiron Temperature and Humidity Sensor"
#define MEMSIC_SENSOR_OBJECT_ID               L"Memsic"
#define MEMSIC_SENSOR_OBJECT_NAME_VALUE       L"Memsic Dual-Axis G-Force Sensor"
#define HITACHI_SENSOR_OBJECT_ID              L"Hitachi"
#define HITACHI_SENSOR_OBJECT_NAME_VALUE      L"Hitachi Tri-Axis G-Force Sensor"
```

这些对象标识符常量会传递到源模块中的方法，这些方法用于处理对象枚举 (*WpdObjectEnum*) 、属性处理 (*WpdObjectProperties*) 和设备功能检索 (*WpdCapabilities。* 下面的 **WpdObjectEnumerator：： OnFindNext** 方法摘录显示了如何在示例驱动程序的对象枚举中使用这些标识符：

```cpp
// If the enumeration context reports that there are more objects to return, then continue, if not,
    // return an empty results set.
    if ((hr == S_OK) && (pEnumeratorContext != NULL) && (pEnumeratorContext->HasMoreChildrenToEnumerate() == TRUE))
    {
        if (pEnumeratorContext->m_strParentObjectID.CompareNoCase(L"") == 0)
        {
            // We are being asked for the WPD_DEVICE_OBJECT_ID
            hr = AddStringValueToPropVariantCollection(pObjectIDCollection, WPD_DEVICE_OBJECT_ID);
            CHECK_HR(hr, "Failed to add 'DEVICE' object ID to enumeration collection");

            // Update the number of children we are returning for this enumeration call
            NumObjectsEnumerated++;
        }
        else if (pEnumeratorContext->m_strParentObjectID.CompareNoCase(WPD_DEVICE_OBJECT_ID) == 0)
        {
    
            // We are being asked for direct children of the WPD_DEVICE_OBJECT_ID
            switch (m_pBaseDriver->m_SensorType)
            {
            case WpdBaseDriver::UNKNOWN:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::COMPASS:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, COMPASS_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::SENSIRON:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, TEMP_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::FLEX:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, FLEX_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::PING:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, PING_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::PIR:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, PIR_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::MEMSIC:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, MEMSIC_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::QTI:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, QTI_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::PIEZO:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, PIEZO_SENSOR_OBJECT_ID);
                    break;
            case WpdBaseDriver::HITACHI:
                    hr = AddStringValueToPropVariantCollection(pObjectIDCollection, HITACHI_SENSOR_OBJECT_ID);
                    break;
                default:
                    break;
```

在 WpdBasicHardwareDriver 示例中，驱动程序定义了包含所有传感器的单一功能类别。 驱动程序开发人员可以扩展此示例，并为每个传感器类型定义单独的功能类别，使应用程序能够识别驱动程序支持的传感器。 这要求开发人员修改 WpdCapabilities：： OnGetFunctionalCategories 方法，使其正确返回这些新类别。

 

 




