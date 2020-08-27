---
description: '支持 WPD 基础结构 (WpdServiceSampleDriverSample) '
title: '支持 WPD 基础结构 (WpdServiceSampleDriverSample) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: defa8bd593cf74c1239e6beced43d71ec004806f
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969542"
---
# <a name="support-for-wpd-infrastructure-wpdservicesampledriversample"></a>支持 WPD 基础结构 (WpdServiceSampleDriverSample) 


WPD 基础结构是命令驱动的。 当 WPD 应用程序调用给定接口中的方法之一时，WPD 序列化程序 (进程内 COM 服务器) 将方法调用转换为它发送到驱动程序的一个或多个命令。 相反，驱动程序将处理这些命令，然后返回响应。 有关基础结构的详细信息，请参阅 [体系结构概述](architecture-overview.md) 主题。

以下 *WpdMon.exe* 工具的图像显示了一个应用程序的结果，该应用程序调用 **IPortableDeviceServiceMethods：： invoke** 方法来调用示例驱动程序所支持的 BeginSync 方法：

![wpd 监视器](images/iportabledeviceservicemethods_invoke_method_wpdmon.png)

在上图中，WPD 序列化程序将 **调用** 调用转换为 WPD \_ 命令 \_ 服务 \_ 方法 \_ START \_ invoke 命令和相应的参数。 驱动程序已处理此命令并向 WPD API 发出两个响应。 第一个响应是 WPD \_ 命令 \_ 服务 \_ 方法启动调用的结果， \_ \_ 以指示 **StartInvoke**命令成功并且该方法已开始在设备上运行。 第二个响应是 \_ \_ \_ \_ 驱动程序在方法完成时发送的 WPD 事件服务方法完成事件。 Driver sent WPD \_ EVENT \_ SERVICE \_ 方法完成， \_ 以便 WPD API 可以执行必要的方法完成和清理。 对于示例驱动程序，这两个响应会立即后跟，无时间延迟;在实际设备上，如果一个方法需要很长时间才能完成，则这两个响应之间可能存在延迟。

WPD \_ 命令 \_ 服务 \_ 方法 \_ \_ 首先在 **WpdService：:D ispatchwpdmessage** 方法中进行处理。 此方法反过来会调用 **WpdServiceMethod：： OnStartInvoke** 方法。 第一种方法可在 *WpdService*文件中找到;第二个在文件 *WpdServiceMethod*中找到。

下面的 **WpdService:D：** *WpdService* 中的 ispatchwpdmessage 方法的以下摘录显示了对 **WpdServiceMethod：： OnStartInvoke** 处理程序的调用。 **DispatchWpdMessage**方法将命令参数传递给处理程序。 这些命令参数由指向 **Invoke** 方法的参数的指针和指向接收方法结果的 *pResults* 变量的指针组成：

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdServiceSampleDriverSample](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





