---
description: '支持 WPD 基础结构 (WpdBasicHardwareDriverSample) '
title: '支持 WPD 基础结构 (WpdBasicHardwareDriverSample) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f267113fa509b400afa9e80338332e5d665c21d4
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969448"
---
# <a name="support-for-wpd-infrastructure-wpdbasichardwaredriversample"></a>支持 WPD 基础结构 (WpdBasicHardwareDriverSample) 


WPD 基础结构是命令驱动的。 当 WPD 应用程序调用给定接口中的方法之一时，WPD 序列化程序 (进程内 COM 服务器) 将方法调用转换为它发送到驱动程序的一个或多个命令。 然后，驱动程序将处理这些命令并返回响应。 有关基础结构的详细信息，请参阅 [体系结构概述](architecture-overview.md) 主题。

以下 *WpdMon.exe* 工具的图像显示了调用 **IPortableDeviceProperties：： GetPropertyAttributes** 方法的应用程序的结果，以检索温度和湿度传感器的属性特性。

![wpd 监视器 ](images/wpdmon_get_attributes.png)

在上图中，WPD 序列化程序将 **GetPropertyAttributes** 调用转换为 WPD \_ COMMAND \_ OBJECT \_ PROPERTIES \_ \_ 命令和相应的参数。 驱动程序处理了此命令，并向 WPD API 发出了响应。

WPD \_ 命令 \_ 对象属性 \_ " \_ 获取 \_ 属性" 命令首先在 **WpdObjectProperties：:D ispatchwpdmessage** 方法中进行处理。 此方法反过来会调用 **WpdObjectProperties：： OnGetPropertyAttributes** 方法。 这两种方法都位于 *WpdObjectProperties* 源文件中。

下面的 **WpdObjectProperties:D：** *WpdObjectProperties* 中的 ispatchwpdmessage 方法的以下摘录显示了对 **WpdObjectProperties：： OnGetPropertyAttributes** 处理程序的调用，以便检索属性特性。 **DispatchWpdMessage**方法将命令参数传递给处理程序。 这些参数包括驱动程序应检索其属性的对象的对象标识符。 此外，参数还包括一个属性键的集合，这些属性键用于标识要检索的特性。

```cpp
HRESULT WpdObjectProperties::DispatchWpdMessage(
    const PROPERTYKEY&     Command,
    IPortableDeviceValues* pParams,
    IPortableDeviceValues* pResults)
{
    HRESULT hr = S_OK;

    if (hr == S_OK)
    {
        if (Command.fmtid != WPD_CATEGORY_OBJECT_PROPERTIES)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, 
                     "This object does not support this command category %ws",
                     CComBSTR(Command.fmtid));
        }
    }

    if (hr == S_OK)
    {
     …
        else if(IsEqualPropertyKey(Command, 
                                   WPD_COMMAND_OBJECT_PROPERTIES_GET_ATTRIBUTES))
        {
            hr = OnGetPropertyAttributes(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to get property attributes");
            }
        }
        …
    return hr;
}
```

**WpdObjectProperties：： OnGetPropertyAttributes**方法返回 (IPortableDeviceValues) 的设备值集合中请求的属性的集合。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





