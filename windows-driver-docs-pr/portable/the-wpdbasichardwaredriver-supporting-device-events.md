---
description: 支持设备事件
title: 支持设备事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5408c93868956cf3927c7e6360ea26884de7566
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969478"
---
# <a name="supporting-device-events"></a>支持设备事件


示例驱动程序定义并支持与传感器功能对象相关联的自定义 WPD 事件，并 \_ 更新 WPD 事件 \_ 传感器 \_ 读数 \_ 。

将发送此自定义事件，通知任何连接的客户端新的传感器读数可用。 下表中的信息介绍参数。

| 参数名称                   | 说明                                                         |
|----------------------------------|---------------------------------------------------------------------|
| WPD \_ 事件 \_ 参数 \_ 事件 \_ ID | 一个 GUID 值，它设置 \_ 为 \_ \_ 已更新的 WPD 事件传感器读数 \_ 。          |
| 传感器 \_ 读数                  | 包含传感器读数的无符号大整数值。   |
| 传感器 \_ 更新 \_ 间隔         | 包含传感器更新间隔的无符号整数值。 |



此自定义事件的事件 GUID 是在 *stdafx.h*中定义的。 在 **WpdBaseDriver 中：:P rocessreaddata**，驱动程序会在提取传感器读数后调用 **WpdBaseDriver：:P ostsensorreadingevent** ，并从读取请求更新间隔，然后将其转换为 DWORD 值。

**WpdBaseDriver：:P ostsensorreadingevent** 完成以下步骤：

1.  初始化 **IPortableDeviceValues** 以保存事件参数。
2.  将 **IPortableDeviceValues** 序列化为字节缓冲区。
3.  调用 **IWDFDevice:P：** EventGuid 设置为 WPD 事件通知的 \_ \_ ，事件类型设置为 WdfEventBroadcast，以及事件参数的序列化字节缓冲区：

```cpp
if (hr == S_OK)
{
    // Initialize the event parameters
    m_pEventParams->Clear();

    // Populate the event parameters
    hr = m_pEventParams-> 
         SetGuidValue(WPD_EVENT_PARAMETER_EVENT_ID, 
                      WPD_EVENT_SENSOR_READING_UPDATED);
    CHECK_HR(hr, "Failed to set the WPD_EVENT_PARAMETER_EVENT_ID");
}

if (hr == S_OK)
{
    hr = m_pEventParams->SetUnsignedLargeIntegerValue(SENSOR_READING, 
                                                 llSensorData);
    CHECK_HR(hr, "Failed to set the sensor reading");
}

if (hr == S_OK)
{
    hr = m_pEventParams->SetUnsignedIntegerValue(SENSOR_UPDATE_INTERVAL, dwUpdateInterval);
    CHECK_HR(hr, "Failed to set the sensor update interval");
}

if (hr == S_OK)
{
    // Create a buffer with the serialized parameters
    hr = m_pWpdSerializer->GetBufferFromIPortableDeviceValues(m_pEventParams,  
                                                              &pBuffer,
                                                              &cbBuffer);
    CHECK_HR(hr, "Failed to get buffer from IPortableDeviceValues");
}
// Send the event
if (hr == S_OK)
{
    hr = m_pWDFDevice->PostEvent(WPD_EVENT_NOTIFICATION, 
                                 WdfEventBroadcast, 
                                 pBuffer, 
                                 cbBuffer);
    CHECK_HR(hr, "Failed to post the WPD broadcast event");
}
```

若要接收任何 WPD 事件，应用程序将实现 **IPortableDeviceEventCallback：： OnEvent** 回调方法，并调用 **IPortableDevice：： Advise** 来注册以接收事件通知回调。

在事件回调中，应用程序检查事件 GUID 是否与更新的 WPD \_ 事件 \_ 传感器读数匹配 \_ \_ ，并从事件参数获取传感器读数和间隔数据。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)









