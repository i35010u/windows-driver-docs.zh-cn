---
title: 设备维护
description: Windows 8.1 和更高版本的 Windows 中引入了设备维护功能。
ms.assetid: 310E92A9-F751-4346-9B2D-0578A136AD20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7491faa741c59a22e93db913bfced97f1d4a1f77
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218219"
---
# <a name="device-maintenance"></a>设备维护


Windows 8.1 和更高版本的 Windows 中引入了设备维护功能。

此功能使用双向通信 () 双向通信，使你能够将 UWP 设备应用或打印机扩展中的设备维护命令发送到打印子系统。 例如，可以将命令发送到打印设备，以清洗墨水喷嘴。

端口监视器与供应商提供的双向扩展文件一起使用，以将这些双向请求转换为设备和特定于协议的命令，然后将它们传输到打印设备。 设备维护任务是通过向打印设备发送双向 "Set" 查询来执行的，而设备的双向响应则指示操作是成功还是失败。

有助于实现此功能的新异步接口采用字符串参数形式的 XML 数据和回调对象。

由于接口是异步的，因此调用方无需等待响应。 完成双向运算后，将调用回调对象。

## <a name="the-new-interfaces"></a>新接口


已在 Windows (名为 "Blue" ) 中引入了以下接口，以实现设备维护功能。

[**IPrinterBidiSetRequestCallback**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterbidisetrequestcallback)

[**IPrinterExtensionAsyncOperation**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensionasyncoperation)

[**IPrinterQueue2**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)

## <a name="initiating-a-device-maintenance-session"></a>启动设备维护会话


若要启动设备维护会话，必须首先创建 XML 数据形式的命令字符串。 然后，必须创建将在异步双向操作完成后调用的回调对象的实例。

完成操作后，将对 IPrinterBidiSetRequestCallback：： Completed 方法调用回调对象，并提供操作的 HRESULT 值。 然后，可以分析此 HRESULT 值并执行任何其他所需的任务。

以下 c # 代码片段概述了如何从 UWP 设备应用程序发出设备维护任务。

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

通过三个入口点中的任何一个调用应用后，UWP 设备应用都支持设备维护。

## <a name="related-topics"></a>相关主题
[**IPrinterBidiSetRequestCallback**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterbidisetrequestcallback)  
[**IPrinterExtensionAsyncOperation**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensionasyncoperation)  
[**IPrinterQueue2**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)