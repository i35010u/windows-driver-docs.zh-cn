---
description: 支持 (WpdBasicHardwareDriverSample) 的属性命令
title: 支持 (WpdBasicHardwareDriverSample) 的属性命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efb2a0b432f155a192cca19a8c21c4e9181cb5d6
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969442"
---
# <a name="supporting-wpd-property-commands-wpdbasichardwaredriversample"></a>支持 WPD 属性命令 (WpdBasicHardwareDriverSample) 


示例驱动程序支持六个属性命令。 这些命令最初由 **WpdObjectProperties：:D ispatchmessage** 方法进行处理，该方法反过来会调用相应的命令处理程序。 **DispatchMessage**方法和单独的处理程序都位于*WpdObjectProperties*文件中。

下表中的信息介绍了每个受支持的属性命令，以及 **WpdObjectProperties：:D ispatchmessage** 在处理给定命令时调用的处理程序的名称。

| Command                                           | Handler                  | 说明                                                                                          |
|---------------------------------------------------|--------------------------|------------------------------------------------------------------------------------------------------|
| \_支持 WPD \_ 命令 \_ 对象 \_ 属性 \_  | OnGetSupportedProperties | 返回给定对象的属性键的数组。                                              |
| WPD \_ 命令 \_ 对象 \_ 属性 \_ GET             | OnGetPropertyValues      | 返回属性值的集合，这些属性值对应于提供给驱动程序的属性键。 |
| WPD \_ 命令 \_ 对象 \_ 属性 \_ 获取 \_ 全部        | OnGetAllProperties       | 返回给定对象的所有属性值。                                                  |
| WPD \_ 命令 \_ 对象 \_ 属性 \_ 集             | OnSetPropertyValues      | 在设备上设置指定的属性值。                                                     |
| WPD \_ 命令 \_ 对象 \_ 属性 \_ 获取 \_ 属性 | OnGetPropertyAttributes  | 返回给定对象的一个或多个属性的特性集合。                     |
| WPD \_ 命令 \_ 对象 \_ 属性 \_ 删除          | OnDeleteProperties       | 删除由指定的属性键标识的属性。                               |



## <a name="span-idwpd_command_object_properties_get_supportedspanspan-idwpd_command_object_properties_get_supportedspanwpd_command_object_properties_get_supported"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET_SUPPORTED"></span><span id="wpd_command_object_properties_get_supported"></span>\_支持 WPD \_ 命令 \_ 对象 \_ 属性 \_


驱动程序调用 **WpdObjectProperties：： OnGetSupportedProperties** 处理程序来响应 WPD \_ command \_ 对象属性 " \_ \_ 获取支持" \_ 命令。 处理程序依次调用 **AddSupportedPropertyKeys** 方法来检索所请求的对象的受支持的键。

由于示例设备不支持 WpdHelloWorldSample 驱动程序中的存储、文件夹或文件对象，并且由于新的驱动程序支持在原始驱动程序中找不到的对象，因此需要更新 **AddSupportedPropertyKeys** 方法。

以下代码取自修改后的 **AddSupportedPropertyKeys** 方法。 此方法将调用两个支持方法 (**AddDevicePropertyKeys** 和 **AddSensorPropertyKeys**) 检索所请求对象的密钥：

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

## <a name="span-idwpd_command_object_properties_getspanspan-idwpd_command_object_properties_getspanwpd_command_object_properties_get"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET"></span><span id="wpd_command_object_properties_get"></span>WPD \_ 命令 \_ 对象 \_ 属性 \_ GET


驱动程序调用 **WpdObjectProperties：： OnGetPropertyValues** 处理程序来响应 WPD \_ COMMAND \_ OBJECT \_ PROPERTIES \_ GET 命令。 进而，处理程序将调用 **GetPropertyValuesForObject** 方法来检索所请求的属性的当前值。 由于传感器设备不支持在 WpdHelloWorldSample 驱动程序中找到的存储、文件夹或文件对象，并且由于新的驱动程序支持在原始驱动程序中找不到的对象，因此需要更新此方法。

返回的设备对象属性的代码保持不变。 这是返回固件版本、电源级别、电源、设备协议、设备型号等的代码。

尽管此代码不变，但该示例驱动程序返回的设备型号 (和其他类似属性) 不同于 WpdHelloWorldSample 驱动程序返回的属性值。 这是因为我们更新了 *WpdObjectProperties*中的定义：

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

下表列出了 *WpdObjectProperties*中的定义、WpdHelloWorldSample 中的原始值以及示例驱动程序中指定的新值。

| 定义                             | 原始值              | 新值                   |
|----------------------------------------|-----------------------------|-----------------------------|
| 设备 \_ 协议 \_ 值                | Hello World 协议5v  | 传感器协议5v       |
| 设备 \_ 固件 \_ 版本              | 1.0.0.0                     | 1.0.0.0                     |
| 设备 \_ 电源 \_ 级别                   | 100                         | 100                         |
| 设备 \_ 型号 \_ 值                   | Hello World!                | RS-232 传感器               |
| 设备 \_ 友好 \_ 名称                 | Hello World!                | 视差 BS2 传感器         |
| 设备 \_ 制造商 \_ 值            | WPD 组                   | WPD 组                   |
| 设备 \_ 序列 \_ 号 \_ 值          | 012345678901234567890123456 | 012345678901234567890123456 |
| 设备 \_ 支持 \_ NONCONSUMABLE \_ 值 | **FALSE**                   | **FALSE**                   |



检索传感器属性的部分中发生了对 **GetPropertyValuesForObject** 方法的最重大更改。 此代码检索 *WpdObjectProperties* 中定义的多个值，例如对象名称、其格式、其内容类型以及是否可将其删除。

此外，此代码还会检索当前传感器读数和传感器更新间隔。 这最后两个属性是通过调用以下两个 helper 函数检索的： **GetSensorReading** 和 **GetUpdateInterval**。

**GetPropertyValuesForObject**方法中的以下摘录包含用于检索传感器对象属性的代码：

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

**GetSensorReading** helper 函数以数字 (DWORD) 格式检索最新的传感器读数：

```cpp
LONGLONG WpdObjectProperties::GetSensorReading()
{    
    // Ensure that this value isn't currently being accessed by another thread
    CComCritSecLock<CComAutoCriticalSection> Lock(m_SensorReadingCriticalSection);

    return m_llSensorReading;
}
```

**注意**  若要防止对 *m \_ llSensorReading* 成员变量的并发访问，必须使用临界区。 此值在每个 RS232 读异步完成时被覆盖，并在 \_ WPD 应用程序检索传感器读取属性时被读取。



**GetUpdateInterval** helper 函数执行相同的操作：它访问*m \_ dwUpdateInterval*成员变量，并以数字 (DWORD) 格式返回值（如果可用）：

```ManagedCPlusPlus
DWORD WpdObjectProperties::GetUpdateInterval()
{    
    return m_dwUpdateInterval;
}
```

请注意，如果有多个线程访问此 (值，则 *m \_ dwUpdateInterval* 成员变量必须受临界区的保护。例如，如果使用了 WDF 并行调度队列而不是顺序调度队列，或 **WpdBaseDriver：:P rocessreaddata** 修改为在初始化) 期间多次设置更新间隔，而不是一次，则为。 为简单起见，将省略临界区。

## <a name="span-idwpd_command_object_properties_get_allspanspan-idwpd_command_object_properties_get_allspanwpd_command_object_properties_get_all"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET_ALL"></span><span id="wpd_command_object_properties_get_all"></span>WPD \_ 命令 \_ 对象 \_ 属性 \_ 获取 \_ 全部


驱动程序将调用 **WpdObjectProperties：： OnGetAllPropertyValues** 处理程序来响应 WPD \_ command \_ 对象属性 \_ " \_ 获取 \_ 全部" 命令。 进而，处理程序会检索给定对象的所有属性键，然后调用 **GetPropertyValuesForObject** helper 函数来检索所请求的属性的当前值。

## <a name="span-idwpd_command_object_properties_setspanspan-idwpd_command_object_properties_setspanwpd_command_object_properties_set"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_SET"></span><span id="wpd_command_object_properties_set"></span>WPD \_ 命令 \_ 对象 \_ 属性 \_ 集


驱动程序调用 **WpdObjectProperties：： OnSetPropertyValues** 处理程序以响应 WPD \_ command \_ OBJECT \_ PROPERTIES \_ SET 命令。 在示例驱动程序中可以编写 (或设置) 的唯一属性是传感器 \_ 更新 \_ 间隔。

处理程序首先检查给定属性的对象标识符，然后检查属性键本身。 如果对象标识符设置为传感器 \_ 对象 \_ ID，并且属性键为传感器 \_ 更新 \_ 间隔，则处理程序将调用 **SendUpdateIntervalToDevice** helper 函数以更新值。

**SendUpdateIntervalToDevice** helper 函数通过检查有效的输入值、使用该值格式化写入请求，然后将写入请求发送到设备来执行写入操作。

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

## <a name="span-idwpd_command_object_properties_get_attributesspanspan-idwpd_command_object_properties_get_attributesspanwpd_command_object_properties_get_attributes"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET_ATTRIBUTES"></span><span id="wpd_command_object_properties_get_attributes"></span>WPD \_ 命令 \_ 对象 \_ 属性 \_ 获取 \_ 属性


驱动程序将调用 **WpdObjectProperties：： OnGetPropertyAttributes** 处理程序以响应 WPD \_ COMMAND \_ 对象属性 \_ " \_ 获取 \_ 属性" 命令。 然后，处理程序将调用 **GetPropertyAttributesForObject** helper 函数来检索给定对象的属性。

在原始 WpdHelloWorldSample 驱动程序中，每个属性的属性都是相同的，并且所有属性都是只读的。 但是，在更新的驱动程序中，传感器 \_ 更新 \_ 间隔为读/写，并且传感器 \_ 更新 \_ 间隔和传感器 \_ 读数的格式为 "WPD \_ 属性" \_ \_ \_ 。 因此，此 helper 函数需要进行少量更改。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)









