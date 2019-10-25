---
title: 处理 UMDF 驱动程序中的客户端模拟
description: 本主题介绍用户模式驱动程序框架（UMDF）驱动程序如何访问受保护的资源，从 UMDF 版本2开始。
ms.assetid: 02EA93CE-3C4D-4F6F-8E58-DD78EBDB19DE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c22fbb8c43a19133dbee065e43b024b0fcea081
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845223"
---
# <a name="handling-client-impersonation-in-umdf-drivers"></a>处理 UMDF 驱动程序中的客户端模拟


本主题介绍用户模式驱动程序框架（UMDF）驱动程序如何访问受保护的资源，从 UMDF 版本2开始。

UMDF 驱动程序通常在 LocalService 帐户下运行，并且无法访问需要用户凭据的文件或资源，如受保护的文件或其他受保护的资源。 UMDF 驱动程序通常对在客户端应用程序和设备之间流动的命令和数据进行操作。 因此，大多数 UMDF 驱动程序不会访问受保护的资源。

但是，某些驱动程序可能需要访问受保护的资源。 例如，UMDF 驱动程序可以通过客户端应用程序提供的文件将固件加载到设备。 此文件可能有一个访问控制列表（ACL），该列表可阻止未经授权的用户修改文件和控制设备。 遗憾的是，此 ACL 还会阻止 UMDF 驱动程序访问该文件。

该框架提供了一种模拟功能，该功能允许驱动程序模拟驱动程序的客户端，并获取客户端对受保护资源的访问权限。

### <a name="enabling-impersonation"></a>启用模拟

UMDF 驱动程序的安装包和客户端应用程序必须启用框架的模拟功能，如下所示：

-   UMDF 驱动程序的安装包的 INF 文件必须包含**UmdfImpersonationLevel**指令并设置允许的最大模拟级别。 仅当 INF 文件包含**UmdfImpersonationLevel**指令时，才启用模拟。 有关设置模拟级别的详细信息，请参阅[在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

-   客户端应用程序必须为每个文件句柄设置允许的模拟级别。 该应用程序使用 Microsoft Win32 **CreateFile**函数中的服务质量（QoS）设置设置允许的模拟级别。 有关这些设置的详细信息，请参阅 Windows SDK 文档中的**CreateFile**的*dwFlagsAndAttributes*参数。

### <a name="handling-impersonation-for-an-io-request"></a>处理 i/o 请求的模拟

UMDF 驱动程序和框架按以下顺序处理 i/o 请求的模拟：

1.  驱动程序调用[**WdfRequestImpersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)方法以指定所需的模拟级别和[*EvtRequestImpersonate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)回调函数。

2.  框架检查请求的模拟级别。 如果请求的级别大于 UMDF 驱动程序的安装包和客户端应用程序允许的级别，则模拟请求会失败。 否则，框架将模拟客户端，并立即调用[*EvtRequestImpersonate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)回调函数。

[*EvtRequestImpersonate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)回调函数必须只执行需要请求的模拟级别的操作，例如打开受保护的文件。

框架不允许驱动程序的[*EvtRequestImpersonate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)回调函数调用框架的任何对象方法。 这可确保驱动程序不会向其他驱动程序回调函数或其他驱动程序公开模拟级别。

最佳做法是，在为该请求调用[**WdfRequestImpersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)之前，驱动程序不应启用对 i/o 请求的[取消](canceling-i-o-requests.md)。

[**WdfRequestImpersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)方法仅授予驱动程序请求的模拟级别。

### <a name="passing-credentials-down-the-driver-stack"></a>沿驱动程序堆栈向下传递凭据

当你的驱动程序收到[**WdfRequestTypeCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_type)类型的 i/o 请求时，驱动程序可能会将该驱动程序堆栈向下移动 i/o 请求。 内核模式驱动程序没有[**WdfRequestImpersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)提供给 UMDF 驱动程序的模拟功能。

因此，如果你希望内核模式驱动程序接收客户端的用户凭据（而不是[驱动程序主机进程](umdf-driver-host-process.md)的凭据），则驱动程序必须设置[**WDF\_请求\_发送\_选项\_模拟\_客户端**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags)在调用[**WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)以将创建请求发送到 i/o 目标时的标志。 如果模拟尝试失败， **Send**方法将返回错误代码，除非该驱动程序还将**WDF\_请求\_发送\_选项\_模拟\_忽略\_失败**标志。

下面的示例演示了 UMDF 驱动程序如何使用**WDF\_请求\_发送\_选项\_模拟\_客户端**标志来向 i/o 目标发送文件创建请求。 驱动程序的 INF 文件还必须包含如上所述的**UmdfImpersonationLevel**指令。

```cpp
WDFIOTARGET iotarget;
WDF_REQUEST_SEND_OPTIONS options;
NTSTATUS status;
WDF_REQUEST_PARAMETERS params;
ULONG sendFlags;  
 
WDF_REQUEST_PARAMETERS_INIT(&params);
WdfRequestGetParameters(Request, &params);
   
sendFlags = WDF_REQUEST_SEND_OPTION_SYNCHRONOUS;
if (params.Type == WdfRequestTypeCreate) {
    sendFlags |= WDF_REQUEST_SEND_OPTION_IMPERSONATE_CLIENT;
}
   
WDF_REQUEST_SEND_OPTIONS_INIT(&options, sendFlags);
if (WdfRequestSend(Request,
                   iotarget,
                   &options
                   ) == FALSE) {
    status = WdfRequestGetStatus(Request);
}
```

在将请求发送到 i/o 目标之前，驱动程序无需调用[**WdfRequestImpersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestimpersonate) 。

如果低级驱动程序还转发请求，客户端的模拟级别会沿着驱动程序堆栈向下传递。

### <a name="reducing-security-threats"></a>降低安全威胁

为了降低 "特权提升" 攻击的几率，你应该：

-   尝试避免使用模拟。

    例如，若要避免使用模拟打开驱动程序必须使用的文件，客户端应用程序可以打开该文件，并使用 i/o 操作将文件内容发送到该驱动程序。

-   使用驱动程序所需的最低模拟级别。

    将驱动程序的 INF 文件中的模拟级别设置为尽可能低。 如果你的驱动程序不需要任何模拟，请不要在 INF 文件中包含**UmdfImpersonationLevel**指令。

-   最大程度地减少攻击者利用驱动程序的机会。

    [*EvtRequestImpersonate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)回调函数应包含一小部分代码，仅执行需要模拟的操作。 例如，如果您的驱动程序访问受保护的文件，则它仅在打开文件句柄时才需要模拟。 它不需要模拟即可读取或写入文件。

 

 





