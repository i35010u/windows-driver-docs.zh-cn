---
Description: Supporting Device Events
title: 支持设备事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 635a977b619c5783b9f60d3f0787e8ad114bf465
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544106"
---
# <a name="supporting-device-events"></a>支持设备事件


示例驱动程序定义并支持与传感器功能对象，WPD 相关联的自定义 WPD 事件\_事件\_传感器\_读取\_已更新。

此自定义事件发送通知任何已连接的客户端新的传感器读数可。 下表中的信息介绍的参数。

| 参数名称                   | 描述                                                         |
|----------------------------------|---------------------------------------------------------------------|
| WPD\_EVENT\_PARAMETER\_EVENT\_ID | GUID 值设置为 WPD\_事件\_传感器\_读取\_已更新。          |
| 传感器\_读取                  | 一个包含传感器读数的无符号大整数值。   |
| 传感器\_更新\_间隔         | 一个包含传感器更新间隔的无符号的整数值。 |



中定义此自定义事件的事件 GUID *Stdafx.h*。 在中**WpdBaseDriver::ProcessReadData**，驱动程序调用**WpdBaseDriver::PostSensorReadingEvent**提取传感器读数后，更新从的读取请求的时间间隔，然后将转换到DWORD 值。

**WpdBaseDriver::PostSensorReadingEvent**完成以下步骤：

1.  初始化**IPortableDeviceValues**来保存事件参数。
2.  序列化为**IPortableDeviceValues**字节缓冲区。
3.  调用**IWDFDevice::PostEvent**具有将 EventGuid 设置为 WPD\_事件\_通知、 事件类型设置为 WdfEventBroadcast 和的事件参数的序列化的字节缓冲区：

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

若要接收的任何 WPD 事件，应用程序会实现**IPortableDeviceEventCallback::OnEvent**回调方法并调用**IPortableDevice::Advise**注册以接收事件通知回调。

在事件回叫，应用程序会检查事件 GUID 是否与匹配 WPD\_事件\_传感器\_读取\_已更新，并获取传感器读取数据和区间数据从事件参数。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)









