---
Description: WPD 基础结构 (WpdBasicHardwareDriverSample) 的支持
title: WPD 基础结构 (WpdBasicHardwareDriverSample) 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4716963f8530b5b4adc7865996c81387010c1392
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387310"
---
# <a name="support-for-wpd-infrastructure-wpdbasichardwaredriversample"></a>WPD 基础结构 (WpdBasicHardwareDriverSample) 的支持


WPD 基础结构是驱动的命令。 当 WPD 应用程序调用的方法之一在给定的接口时，WPD 序列化程序 （进程内 COM 服务器） 将它发送到该驱动程序的一个或多个命令转换为方法调用。 然后，驱动程序处理这些命令，并返回响应。 有关基础结构的详细信息，请参阅[体系结构概述](architecture-overview.md)主题。

下图的*WpdMon.exe*工具显示的应用程序调用结果**IPortableDeviceProperties::GetPropertyAttributes**方法来检索该属性的属性温度和湿度传感器。

![wpd 监视器 ](images/wpdmon_get_attributes.png)

在上图中，转换 WPD 序列化程序**GetPropertyAttributes**调入 WPD\_命令\_对象\_属性\_获取\_属性命令和相应的参数。 该驱动程序处理此命令，并且颁发 WPD API 的响应。

WPD\_命令\_对象\_属性\_获取\_属性命令首先处理中**WpdObjectProperties::DispatchWpdMessage**方法。 此方法，反过来，调用**WpdObjectProperties::OnGetPropertyAttributes**方法。 这两种方法中找到*WpdObjectProperties.cpp*源文件。

中的以下节选**WpdObjectProperties::DispatchWpdMessage**中的方法*WpdObjectProperties.cpp*演示了调用**WpdObjectProperties::OnGetPropertyAttributes**用于检索属性的特性的处理程序。 **DispatchWpdMessage**方法将命令参数传递给处理程序。 这些参数包括驱动程序应检索其属性的对象的对象标识符。 此外，参数包括标识要检索的属性的属性键的集合。

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

**WpdObjectProperties::OnGetPropertyAttributes**方法返回的请求的属性集合中的设备值 (IPortableDeviceValues) 的集合。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





