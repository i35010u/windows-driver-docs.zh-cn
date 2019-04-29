---
title: 设备维护
description: 在 Windows 8.1 和更高版本的 Windows 中引入了设备维护功能。
ms.assetid: 310E92A9-F751-4346-9B2D-0578A136AD20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b654b230e1fa593635e19c189f3b6dd1c6cd070
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365343"
---
# <a name="device-maintenance"></a>设备维护


在 Windows 8.1 和更高版本的 Windows 中引入了设备维护功能。

此功能使用双向通信 (Bidi) 允许您发送从设备维护命令 UWP 设备应用，或者打印子系统的打印机扩展中。 例如，可以将命令发送到您的打印设备要清洗的墨迹喷嘴。

端口监视器协同工作的供应商提供 Bidi 扩展文件以这些 Bidi 请求转换为设备和特定于协议的命令，然后将其传输给打印设备。 设备维护任务执行的将 Bidi"Set"查询发送到打印设备，以及来自设备的 Bidi 响应指示该操作是成功还是失败。

可帮助实现此功能的新异步接口接收的 XML 数据形式的字符串参数和回调对象。

此接口是异步的因为调用方不必等待响应。 Bidi 操作完成后，会调用的回调对象。

## <a name="the-new-interfaces"></a>新接口


在 Windows （代号为"蓝色"） 来实现设备维护功能中引入了以下接口。

[**IPrinterBidiSetRequestCallback**](https://msdn.microsoft.com/library/windows/hardware/dn265385)

[**IPrinterExtensionAsyncOperation**](https://msdn.microsoft.com/library/windows/hardware/dn265387)

[**IPrinterQueue2**](https://msdn.microsoft.com/library/windows/hardware/dn265389)

## <a name="initiating-a-device-maintenance-session"></a>启动设备维护会话


若要启动设备维护会话，您必须先创建 XML 数据形式的命令字符串。 然后必须创建异步的双向操作完成后将调用的回调对象的实例。

在操作完成后，在 IPrinterBidiSetRequestCallback::Completed 方法中，调用的回调对象，它提供操作的 HRESULT 值。 然后可以分析此 HRESULT 值，并执行任何其他所需的任务。

以下C#代码片段概述了如何发出从 UWP 设备应用的设备维护任务。

```csharp
//
// Declare a global constant that will be used
// to determine whether method calls were successful
//
const int S_OK = 0;
 
class BidiSendAsyncDemo
{
    //
    // Create a queue object and also
    // create the command string
    //
    void PerformDeviceMaintenance(
        IPrinterQueue2 queue,
        string bidiRequestInXml
        )
    {
        BidiSetResultCallback callBack = new BidiSetResultCallback();

        IPrinterExtensionAsyncOperation asyncOperation =
          queue.SendBidiSetRequestAsync(bidiRequestInXml, callBack);
    }
}

/// <summary>
/// This class represents the callback object
/// </summary>
public class BidiSetResultCallback :
    IPrinterBidiSetRequestCallback
{
    void Completed(
        string bidiResponse,
        int hr
        )
    {
        if (S_OK == hr)
        {
            // parse and interpret 'bidiResponse'
        }
    }
} 
```

通过三个入口点的任何调用应用程序后，设备维护支持 UWP 设备应用中。

## <a name="related-topics"></a>相关主题
[**IPrinterBidiSetRequestCallback**](https://msdn.microsoft.com/library/windows/hardware/dn265385)  
[**IPrinterExtensionAsyncOperation**](https://msdn.microsoft.com/library/windows/hardware/dn265387)  
[**IPrinterQueue2**](https://msdn.microsoft.com/library/windows/hardware/dn265389)  



