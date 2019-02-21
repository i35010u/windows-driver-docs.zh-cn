---
Description: Defining the Sensor Objects
title: 定义传感器对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a61abc0fa1324a82750a909d552971e675a0b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519760"
---
# <a name="defining-the-sensor-objects"></a>定义传感器对象


在 Windows 便携式设备 (WPD)，在设备上的逻辑实体称为对象。 对象可以表示设备的信息性消息或功能的部分。 任何对象都具有一个或多个属性。 您可以将属性作为对象说明元数据。 例如，示例温度和湿度传感器上的 TempHumidity 对象支持传感器\_读取属性。 此属性指定的当前温度和相对湿度而获得的设备。

WpdHelloWorldDriver 支持下表中所示的对象。

| 对象  | 描述                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| 设备  | 包含描述性属性，例如根对象、 固件版本、 模型和友好名称。 |
| 存储 | 公开一些属性，例如对象、 存储容量、 文件系统类型和可用的字节数。         |
| 文件夹  | 一个对象，公开一些属性，例如，文件夹名称。                                                             |
| 文件    | 对象公开属性，例如，一个文件名和实际的文件内容。                                      |

 

存储、 文件夹或文件对象不支持示例传感器，因为 WpdBasicHardwareDriver 未实现这些对象。 相反，每个传感器类型表示由单个对象。 下表列出了 WpdBasicHardwareDriver 支持的对象。

| 对象       | 描述                                                                                                                                |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| 设备       | 包含描述性属性，例如根对象、 固件版本、 模型和友好名称。                 |
| TempHumidity | 读取的温度和湿度读取，以及可编辑的更新间隔属性将显示一个功能对象。 |
| 指南针      | 显示指南针读数，以及一个更新间隔属性可编辑的功能对象。                          |
| PIR          | 显示被动红外读取，可以编辑的更新间隔属性以及一个函数对象。                 |
| QTI          | 显示环境光线阅读，可以编辑的更新间隔属性以及一个函数对象。                    |
| 弹性         | 显示读取，压力的功能对象，以及可编辑的更新间隔属性。                         |
| Ping         | 显示读取的距离的函数对象，以及可编辑的更新间隔属性。                         |
| Piezo        | 显示读取，振动的功能对象，以及可编辑的更新间隔属性。                        |
| Memsic       | 显示两个轴加速感应器读取，一个函数对象，以及可编辑的更新间隔属性。             |
| 人： Hitachi      | 显示 3 轴加速感应器读取，一个函数对象，以及可编辑的更新间隔属性。             |

 

在 WPD，对象标识的字符串。 中定义的设备对象的字符串标识符*Portabledevice.h*文件：

```cpp
#define WPD_DEVICE_OBJECT_ID  L"DEVICE"
```

在中定义的传感器对象的字符串标识符*WpdObjectProperties.h* WpdBasicHardwareDriver 文件：

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

这些对象标识符常量传递给处理对象枚举的源代码模块中的方法 (*WpdObjectEnum.cpp*)，属性处理 (*WpdObjectProperties.cpp*)，并设备功能检索 (*WpdCapabilities.cpp*)。 中的以下节选**WpdObjectEnumerator::OnFindNext**方法说明如何使用这些标识符对象枚举中的示例驱动程序：

```cpp
// If the enumeration context reports that there are more objects to return, then continue, if not,
    // return an empty results set.
    if ((hr == S_OK) && (pEnumeratorContext != NULL) && (pEnumeratorContext->HasMoreChildrenToEnumerate() == TRUE))
    {
        if (pEnumeratorContext->m_strParentObjectID.CompareNoCase(L"") == 0)
        {
            // We are being asked for the WPD_DEVICE_OBJECT_ID
            hr = AddStringValueToPropVariantCollection(pObjectIDCollection, WPD_DEVICE_OBJECT_ID);
            CHECK_HR(hr, "Failed to add &#39;DEVICE&#39; object ID to enumeration collection");

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

在 WpdBasicHardwareDriver 示例中，该驱动程序定义单个功能类别包含的所有传感器。 驱动程序开发人员可以扩展此示例，并定义单独的功能类别，为每个传感器类型，以便应用程序可以确定哪些传感器驱动程序支持。 这要求开发人员修改 WpdCapabilities::OnGetFunctionalCategories 方法，以便它将正确返回这些新类别。

 

 




