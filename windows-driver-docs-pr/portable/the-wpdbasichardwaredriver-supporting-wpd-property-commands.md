---
Description: 对属性命令 (WpdBasicHardwareDriverSample) 的支持
title: 对属性命令 (WpdBasicHardwareDriverSample) 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f274fbb67066cc9a3e5937f13079b3d77c255d41
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349954"
---
# <a name="supporting-wpd-property-commands-wpdbasichardwaredriversample"></a>支持 WPD 属性命令 (WpdBasicHardwareDriverSample)


示例驱动程序支持六个属性命令。 这些命令处理最初由**WpdObjectProperties::DispatchMessage**方法，反过来，将调用相应的命令处理程序。 **DispatchMessage**方法和单个处理程序全部位于*WpdObjectProperties.cpp*文件。

下表中的信息描述了每个受支持的属性的命令，以及处理程序的名称， **WpdObjectProperties::DispatchMessage**处理给定的命令时调用。

| Command                                           | 处理程序                  | 描述                                                                                          |
|---------------------------------------------------|--------------------------|------------------------------------------------------------------------------------------------------|
| WPD\_命令\_对象\_属性\_获取\_支持  | OnGetSupportedProperties | 返回给定对象的属性键的数组。                                              |
| WPD\_命令\_对象\_属性\_获取             | OnGetPropertyValues      | 返回提供给该驱动程序的属性键相对应的属性值的集合。 |
| WPD\_命令\_对象\_属性\_获取\_所有        | OnGetAllProperties       | 返回给定对象的所有属性值。                                                  |
| WPD\_命令\_对象\_属性\_设置             | OnSetPropertyValues      | 在设备上设置指定的属性值。                                                     |
| WPD\_命令\_对象\_属性\_获取\_属性 | OnGetPropertyAttributes  | 返回给定对象上的一个或多个属性的特性的集合。                     |
| WPD\_命令\_对象\_属性\_删除          | OnDeleteProperties       | 删除由给定的属性键标识的属性。                               |



## <a name="span-idwpdcommandobjectpropertiesgetsupportedspanspan-idwpdcommandobjectpropertiesgetsupportedspanwpdcommandobjectpropertiesgetsupported"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET_SUPPORTED"></span><span id="wpd_command_object_properties_get_supported"></span>WPD\_命令\_对象\_属性\_获取\_支持


驱动程序调用**WpdObjectProperties::OnGetSupportedProperties**处理程序以响应 WPD\_命令\_对象\_属性\_获取\_支持的命令。 该处理程序依次调用**AddSupportedPropertyKeys**方法来检索所请求的对象的受支持的密钥。

因为示例设备不支持在 WpdHelloWorldSample 驱动程序存储、 文件夹或文件对象，因为新的驱动程序支持原始驱动程序中找不到的对象，更新**AddSupportedPropertyKeys**的方法是有必要。

执行下面的代码从修改后**AddSupportedPropertyKeys**方法。 此方法调用两个支持的方法 (**AddDevicePropertyKeys**并**AddSensorPropertyKeys**) 来检索所请求的对象的密钥：

```cpp
HRESULT AddSupportedPropertyKeys(
    LPCWSTR                        wszObjectID,
    IPortableDeviceKeyCollection*  pKeys)
{
    HRESULT     hr          = S_OK;
    CAtlStringW strObjectID = wszObjectID;

    // Add Common PROPERTYKEYs for ALL WPD objects
    AddCommonPropertyKeys(pKeys);

    if (strObjectID.CompareNoCase(WPD_DEVICE_OBJECT_ID) == 0)
    {
        // Add the PROPERTYKEYs for the 'DEVICE' object
        AddDevicePropertyKeys(pKeys);
    }

    // Add other PROPERTYKEYs for other supported objects...
    if (
           (strObjectID.CompareNoCase(SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(TEMP_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(FLEX_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(PIR_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(PING_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(QTI_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(MEMSIC_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(HITACHI_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(PIEZO_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(COMPASS_SENSOR_OBJECT_ID) == 0)
       )
    {
        // Add the PROPERTYKEYs for the Sensor object
        AddSensorPropertyKeys(pKeys);
    }

    return hr;
}
```

## <a name="span-idwpdcommandobjectpropertiesgetspanspan-idwpdcommandobjectpropertiesgetspanwpdcommandobjectpropertiesget"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET"></span><span id="wpd_command_object_properties_get"></span>WPD\_命令\_对象\_属性\_获取


驱动程序调用**WpdObjectProperties::OnGetPropertyValues**处理程序以响应 WPD\_命令\_对象\_属性\_GET 命令。 该处理程序，反过来，调用**GetPropertyValuesForObject**方法来检索请求的属性的当前值。 因为传感器设备不支持在 WpdHelloWorldSample 驱动程序中, 找到的存储、 文件夹或文件对象，因为新的驱动程序支持的原始的驱动程序中未找到的对象，更新此方法是必需的。

返回设备对象的属性的代码保持不变。 这是返回固件版本、 功率级别、 电源、 设备协议、 设备模型等的代码。

虽然此代码不变，但设备模型 （和其他相似的属性） 返回的示例驱动程序将不同于由 WpdHelloWorldSample 驱动程序返回的属性值。 这是因为我们更新中的定义*WpdObjectProperties.h*:

```cpp
#define DEVICE_PROTOCOL_VALUE                L"Sensor Protocol ver 1.00"
#define DEVICE_FIRMWARE_VERSION_VALUE        L"1.0.0.0"
#define DEVICE_POWER_LEVEL_VALUE             100
#define DEVICE_MODEL_VALUE                   L"RS232 Sensor"
#define DEVICE_FRIENDLY_NAME_VALUE           L"Parallax BS2 Sensor"
#define DEVICE_MANUFACTURER_VALUE            L"Windows Portable Devices Group"
#define DEVICE_SERIAL_NUMBER_VALUE           L"01234567890123-45676890123456"
#define DEVICE_SUPPORTS_NONCONSUMABLE_VALUE  FALSE
```

下表列出了中的定义*WpdObjectProperties.h*，WpdHelloWorldSample 中的原始值和新的示例驱动程序中指定的值。

| 定义                             | 原始值              | 新值                   |
|----------------------------------------|-----------------------------|-----------------------------|
| 设备\_协议\_值                | Hello World Protocol v1.00  | 传感器协议 v1.00       |
| 设备\_固件\_版本              | 1.0.0.0                     | 1.0.0.0                     |
| DEVICE\_POWER\_LEVEL                   | 100                         | 100                         |
| 设备\_模型\_值                   | 世界您好！                | RS-232 传感器               |
| 设备\_友好\_名称                 | 世界您好！                | 视差 BS2 传感器         |
| 设备\_制造商\_值            | WPD 组                   | WPD 组                   |
| DEVICE\_SERIAL\_NUMBER\_VALUE          | 012345678901234567890123456 | 012345678901234567890123456 |
| 设备\_支持\_NONCONSUMABLE\_值 | **FALSE**                   | **FALSE**                   |



最重大更改**GetPropertyValuesForObject**方法检索传感器属性部分中没有发生。 此代码检索中定义的多个值*WpdObjectProperties.h*如对象名称、 其格式、 其内容类型是否可以将其删除。

此外，此代码还会检索当前的传感器读数和传感器更新间隔。 通过调用两个帮助程序函数检索这些最后两个属性：**GetSensorReading**并**GetUpdateInterval**。

中的以下节选**GetPropertyValuesForObject**方法包含检索的传感器对象的属性的代码：

```cpp
// Retrieve the sensor properties

        else if (
                    (strObjectID.CompareNoCase(SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(TEMP_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(FLEX_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(PIR_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(PING_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(QTI_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(MEMSIC_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(HITACHI_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(PIEZO_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(COMPASS_SENSOR_OBJECT_ID) == 0)
                 )
        {
            for (DWORD dwIndex = 0; dwIndex < cKeys; dwIndex++)
            {
                PROPERTYKEY Key = WPD_PROPERTY_NULL;
                hr = pKeys->GetAt(dwIndex, &Key);
                CHECK_HR(hr, "Failed to get PROPERTYKEY at index %d in collection", dwIndex);

                if (hr == S_OK)
                {
                    // Preset the property value to 'error not supported'.  The actual value
                    // will replace this value, if read from the device.
                    pValues->SetErrorValue(Key, HRESULT_FROM_WIN32(ERROR_NOT_SUPPORTED));
                    if (IsEqualPropertyKey(Key, WPD_OBJECT_ID))
                    {
                        hr = pValues->SetStringValue(WPD_OBJECT_ID, strObjectID);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_ID");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_PERSISTENT_UNIQUE_ID))
                    {

                        // Retrieve the ID of the sensor using the m_SensorType member of the
                        // basedriver that is set during the data-read operation.
                        hr = pValues->SetStringValue(WPD_OBJECT_PERSISTENT_UNIQUE_ID, strObjectID);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_PERSISTENT_UNIQUE_ID");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_PARENT_ID))
                    {
                        hr = pValues->SetStringValue(WPD_OBJECT_PARENT_ID, WPD_DEVICE_OBJECT_ID);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_PARENT_ID");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_NAME))
                    {
                        // Retrieve the name of the sensor using the m_SensorType member of the
                        // basedriver that is set during the data-read operation.
                        if (m_pBaseDriver->m_SensorType == 0)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 2)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, TEMP_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 3)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, FLEX_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 4)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, PING_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 5)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, PIR_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 6)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, MEMSIC_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 7)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, QTI_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 8)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, PIEZO_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 9)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, HITACHI_SENSOR_OBJECT_NAME_VALUE);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_NAME");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_FORMAT))
                    {
                        hr = pValues->SetGuidValue(WPD_OBJECT_FORMAT, WPD_OBJECT_FORMAT_UNSPECIFIED);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_FORMAT");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_CONTENT_TYPE))
                    {
                        hr = pValues->SetGuidValue(WPD_OBJECT_CONTENT_TYPE, WPD_CONTENT_TYPE_FUNCTIONAL_OBJECT);
CHECK_HR(hr, "Failed to set WPD_OBJECT_CONTENT_TYPE");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_CAN_DELETE))
                    {
                        hr = pValues->SetBoolValue(WPD_OBJECT_CAN_DELETE, FALSE);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_CAN_DELETE");
                    }

                    else if (IsEqualPropertyKey(Key, SENSOR_READING))
                    {
                        hr = pValues->SetUnsignedLargeIntegerValue(SENSOR_READING, GetSensorReading());
                        CHECK_HR(hr, "Failed to set SENSOR_READING");
                    }

                    else if (IsEqualPropertyKey(Key, SENSOR_UPDATE_INTERVAL))
                    {
                        hr = pValues->SetUnsignedLargeIntegerValue(SENSOR_UPDATE_INTERVAL, GetUpdateInterval());
                        CHECK_HR(hr, "Failed to set SENSOR_UPDATE_INTERVAL");
                    }
                    else if (IsEqualPropertyKey(Key, WPD_FUNCTIONAL_OBJECT_CATEGORY))
                    {
                        hr = pValues->SetGuidValue(WPD_FUNCTIONAL_OBJECT_CATEGORY, FUNCTIONAL_CATEGORY_SENSOR_SAMPLE);
                        CHECK_HR(hr, "Failed to set WPD_FUNCTIONAL_OBJECT_CATEGORY");
                    }
                }
             } // end for
        } // end else if
```

**GetSensorReading**帮助程序函数检索最新的传感器读数 (DWORD) 的数字格式中：

```cpp
LONGLONG WpdObjectProperties::GetSensorReading()
{    
    // Ensure that this value isn't currently being accessed by another thread
    CComCritSecLock<CComAutoCriticalSection> Lock(m_SensorReadingCriticalSection);

    return m_llSensorReading;
}
```

**请注意**临界区是防止并发访问的所需*m\_llSensorReading*成员变量。 每次 RS232 读取以异步方式完成时，会覆盖此值，每当读取传感器\_WPD 应用程序检索读取属性。



**GetUpdateInterval**帮助程序函数执行相同操作： 它将访问*m\_dwUpdateInterval*成员变量并返回它是否格式的数字 (DWORD) 值可用：

```ManagedCPlusPlus
DWORD WpdObjectProperties::GetUpdateInterval()
{    
    return m_dwUpdateInterval;
}
```

请注意， *m\_dwUpdateInterval*成员变量必须受关键部分，如果多个线程将访问此值 （如果为例，而不是顺序使用 WDF 并行调度队列调度队列，或者如果**WpdBaseDriver::ProcessReadData**修改设置多次而不是在初始化过程中一次的更新间隔)。 为简单起见，省略了关键部分。

## <a name="span-idwpdcommandobjectpropertiesgetallspanspan-idwpdcommandobjectpropertiesgetallspanwpdcommandobjectpropertiesgetall"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET_ALL"></span><span id="wpd_command_object_properties_get_all"></span>WPD\_命令\_对象\_属性\_获取\_所有


驱动程序调用**WpdObjectProperties::OnGetAllPropertyValues**处理程序以响应 WPD\_命令\_对象\_属性\_获取\_所有命令. 处理程序，反过来，检索所有属性的给定对象的密钥，然后调用**GetPropertyValuesForObject**帮助程序函数检索请求的属性的当前值。

## <a name="span-idwpdcommandobjectpropertiessetspanspan-idwpdcommandobjectpropertiessetspanwpdcommandobjectpropertiesset"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_SET"></span><span id="wpd_command_object_properties_set"></span>WPD\_命令\_对象\_属性\_设置


驱动程序调用**WpdObjectProperties::OnSetPropertyValues**处理程序以响应 WPD\_命令\_对象\_属性\_SET 命令。 可以编写 （或设置） 中的示例驱动程序的唯一属性是传感器\_更新\_间隔。

该处理程序首先会检查给定属性的对象标识符，然后检查本身的属性键。 如果对象标识符设置为传感器\_对象\_ID 和属性键是传感器\_更新\_间隔，处理程序调用**SendUpdateIntervalToDevice**帮助程序若要更新的值的函数。

**SendUpdateIntervalToDevice**帮助程序函数通过检查有效的输入值、 格式设置写入请求具有此值，并将发送到设备的写入请求执行写入操作。

```cpp
HRESULT WpdObjectProperties::SendUpdateIntervalToDevice(DWORD dwNewInterval)
{
    HRESULT      hr                           = S_OK;
    RS232Target* pDeviceTarget                = NULL;

    CHAR  szInterval[INTERVAL_DATA_LENGTH+1]  = {0};

    // Check the input value
    if (IsValidUpdateInterval(dwNewInterval) == FALSE)
    {
        hr = HRESULT_FROM_WIN32(ERROR_INVALID_DATA);
        CHECK_HR(hr, "Invalid update interval: %d", dwNewInterval);
    }

    // Format a write request with the input value
    if (hr == S_OK)
    {
        hr = StringCchPrintfA(szInterval, 
                              ARRAYSIZE(szInterval), "%d", dwNewInterval);
        CHECK_HR(hr, "Failed to convert the new interval to a CHAR string");
    }

    // Send the write request to the device
    if (hr == S_OK)
    {
        pDeviceTarget = m_pBaseDriver->GetRS232Target();

        if (pDeviceTarget->IsReady())
        {
            hr = pDeviceTarget->
                 SendWriteRequest((BYTE *)szInterval, sizeof(szInterval));
            CHECK_HR(hr, 
                     "Failed to send the write request to 
                      set the new temperature update interval");

            if (hr == S_OK)
            {
                TraceEvents(TRACE_LEVEL_VERBOSE, TRACE_FLAG_DRIVER, 
                            "%!FUNC! Sent new interval: %s", szInterval);
            }
        }
        else
        {
            hr = HRESULT_FROM_WIN32(ERROR_NOT_READY);
            CHECK_HR(hr, "Device is not ready to receive write requests");
        }
    }

    if (hr == S_OK)
    {
        // Update the cached value on the driver
        SetUpdateInterval(dwNewInterval);
    }

    return hr;
}
```

## <a name="span-idwpdcommandobjectpropertiesgetattributesspanspan-idwpdcommandobjectpropertiesgetattributesspanwpdcommandobjectpropertiesgetattributes"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET_ATTRIBUTES"></span><span id="wpd_command_object_properties_get_attributes"></span>WPD\_命令\_对象\_属性\_获取\_属性


驱动程序调用**WpdObjectProperties::OnGetPropertyAttributes**处理程序以响应 WPD\_命令\_对象\_属性\_获取\_属性命令。 该处理程序，反过来，调用**GetPropertyAttributesForObject** helper 函数来检索给定对象的属性。

在原始 WpdHelloWorldSample 驱动程序，每个属性的属性完全相同，所有属性都是只读的。 但是，在更新的驱动程序，传感器\_更新\_间隔是读/写，而这两个传感器\_更新\_间隔和传感器\_读取具有窗体 WPD\_属性\_特性\_窗体\_范围。 因此，此帮助器函数中要求细微的更改。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)









