---
Description: WPD 基础结构 (WpdServiceSampleDriverSample) 的支持
title: WPD 基础结构 (WpdServiceSampleDriverSample) 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe81c865bfd908cef9689ba1d910b801508eb81d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370485"
---
# <a name="support-for-wpd-infrastructure-wpdservicesampledriversample"></a>WPD 基础结构 (WpdServiceSampleDriverSample) 的支持


WPD 基础结构是驱动的命令。 当 WPD 应用程序调用的方法之一在给定的接口时，WPD 序列化程序 （进程内 COM 服务器） 将它发送到该驱动程序的一个或多个命令转换为方法调用。 该驱动程序，反过来，处理这些命令，，然后返回响应。 有关基础结构的详细信息，请参阅[体系结构概述](architecture-overview.md)主题。

下图的*WpdMon.exe*工具显示的应用程序调用结果**IPortableDeviceServiceMethods::Invoke**方法来调用受 BeginSync 方法示例驱动程序：

![wpd 监视器](images/iportabledeviceservicemethods_invoke_method_wpdmon.png)

在上图中，转换 WPD 序列化程序**Invoke**调入 WPD\_命令\_服务\_方法\_启动\_INVOKE 命令和相应的参数。 该驱动程序处理此命令，并且颁发 WPD api 的两个响应。 第一个响应是结果的 WPD\_命令\_服务\_方法\_启动\_调用以指示**StartInvoke**命令已成功，在方法启动设备上运行。 第二个响应是 WPD\_事件\_服务\_方法\_完成时完成的方法，该驱动程序发送的事件。 该驱动程序发送 WPD\_事件\_服务\_方法\_完成，以便 WPD API 可以执行必要的方法完成和清理。 对于示例驱动程序，两个响应遵循立即且没有任何时间延迟;在实际设备上，可以延迟之间有两个响应，如果某方法采用较长时间才能完成。

WPD\_命令\_服务\_方法\_启动\_INVOKE 命令首先处理中**WpdService::DispatchWpdMessage**方法。 此方法，反过来，调用**WpdServiceMethod::OnStartInvoke**方法。 第一种方法在文件中找到*WpdService.cpp*; 第二个在文件中找到*WpdServiceMethod.cpp*。

中的以下节选**WpdService::DispatchWpdMessage**中的方法*WpdService.cpp*演示了调用**WpdServiceMethod::OnStartInvoke**处理程序。 **DispatchWpdMessage**方法将命令参数传递给处理程序。 这些命令参数中包含的参数指向的指针**Invoke**方法，以及一个指向*pResults*接收方法结果的变量：

```cpp
HRESULT WpdService::DispatchWpdMessage(
            REFPROPERTYKEY         Command,
    __in    IPortableDeviceValues* pParams,
    __out   IPortableDeviceValues* pResults)
{
    HRESULT     hr                  = S_OK;
    LPWSTR      pszRequestFilename  = NULL;

    // Get the request filename to process the service message
    hr = pParams->GetStringValue(PRIVATE_SAMPLE_DRIVER_REQUEST_FILENAME, &pszRequestFilename);
    if (FAILED(hr))
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Failed to get the required requested filename");
    }

    if (hr == S_OK)
    {    
        hr = CheckRequestFilename(pszRequestFilename);
        CHECK_HR(hr, "Unknown request filename %ws received", pszRequestFilename);
    }

    if (hr == S_OK)
    {
     …
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_SERVICE_METHODS_START_INVOKE))
        {
            hr = m_ServiceMethods.OnStartInvoke(pParams, pResults);
        }
        …
    return hr;
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[The WpdServiceSampleDriverSample](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





