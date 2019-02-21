---
title: 在 UMDF 1.x 驱动程序中处理客户端模拟
description: 在 UMDF 1.x 驱动程序中处理客户端模拟
ms.assetid: 25beab8c-e6b8-479b-ad60-fcc3b5b56a6d
keywords:
- 用户模式驱动程序框架 WDK 模拟
- UMDF WDK 模拟
- 用户模式驱动程序 WDK UMDF，模拟
- 模拟 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 329f57369e88186a9dcc750ed11fac48b4003a98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546934"
---
# <a name="handling-client-impersonation-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中处理客户端模拟


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF 驱动程序通常在 LocalService 帐户下运行，并且无法访问文件或资源需要用户凭据，如受保护的文件或其他受保护的资源。 通常，UMDF 驱动程序对命令和客户端应用程序和设备之间流动的数据。 因此，大多数 UMDF 驱动程序不访问受保护的资源。

但是，某些驱动程序可能需要对受保护资源的访问。 例如，UMDF 驱动程序可能会加载到的文件中的客户端应用程序提供了设备的固件。 该文件可能具有防止未授权的用户修改的文件和控制的设备的访问控制列表 (ACL)。 遗憾的是，此 ACL 还可阻止 UMDF 驱动程序访问该文件。

该框架提供一种模拟功能，允许驱动程序，以模拟驱动程序的客户端并获取对受保护资源的客户端的访问权限。

### <a name="enabling-impersonation"></a>启用模拟

UMDF 驱动程序的安装包和客户端应用程序必须按如下所示启用框架的模拟功能：

-   UMDF 驱动程序的安装包的 INF 文件必须包含**UmdfImpersonationLevel**指令和组的最大允许的模拟级别。 仅当该 INF 文件包括启用模拟**UmdfImpersonationLevel**指令。 有关设置的模拟级别的详细信息，请参阅[INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

-   客户端应用程序必须设置为每个文件句柄允许的模拟级别。 在 Microsoft Win32 应用程序使用服务质量 (QoS) 设置**CreateFile**函数设置允许的模拟级别。 有关这些设置的详细信息，请参阅*dwFlagsAndAttributes*的参数**CreateFile** Windows SDK 文档中。

### <a name="handling-impersonation-for-an-io-request"></a>处理 I/O 请求的模拟

UMDF 驱动程序和框架处理以下序列中的 I/O 请求的模拟：

1.  驱动程序调用[ **IWDFIoRequest::Impersonate** ](https://msdn.microsoft.com/library/windows/hardware/ff559136)方法，以指定所需的模拟级别和一个[ **IImpersonateCallback::OnImpersonate**](https://msdn.microsoft.com/library/windows/hardware/ff554916)回调函数。

2.  该框架会将请求的模拟级别。 如果所请求的级别大于 UMDF 驱动程序的安装包和客户端应用程序允许的级别，模拟请求失败。 否则为该框架模拟客户端并立即调用**OnImpersonate**回调函数。

**OnImpersonate**回调函数必须在执行需要的请求的模拟级别，例如打开受保护的文件的操作。

UMDF 不允许的驱动程序**OnImpersonate**要调用的任何框架的对象方法的回调函数。 这可确保该驱动程序不会公开给其他驱动程序回调函数或其他驱动程序的模拟级别。

**请注意**  在版本 1.0 到 UMDF，1.7 [ **IWDFIoRequest::Impersonate** ](https://msdn.microsoft.com/library/windows/hardware/ff559136)授予的最高的模拟级别，客户端应用程序和 INF 文件允许，甚至如果该驱动程序请求的模拟级别较低。 在 UMFD 版本 1.9 及更高版本， **Impersonate**方法授予仅模拟级别，则该驱动程序请求。

 

### <a name="passing-credentials-down-the-driver-stack"></a>将驱动程序堆栈的下层的凭据传递

当您的驱动程序收到[ **WdfRequestCreate**](https://msdn.microsoft.com/library/windows/hardware/ff561467)-类型化的 I/O 请求，该驱动程序可能会转发到内核模式驱动程序在驱动程序堆栈的下层的 I/O 请求。 内核模式驱动程序不具有模拟功能， **IWDFIoRequest::Impersonate**提供对基于 UMDF 驱动程序。

因此，如果你想要接收客户端的用户凭据的内核模式驱动程序 (而不是凭据[驱动程序主机进程](umdf-driver-host-process.md))，该驱动程序必须设置[ **WDF\_请求\_发送\_选项\_IMPERSONATE\_客户端**](https://msdn.microsoft.com/library/windows/hardware/ff561462)标志时，它调用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)发送创建对 I/O 目标请求。 **发送**方法将返回错误代码如果模拟尝试失败，除非该驱动程序还会设置**WDF\_请求\_发送\_选项\_模拟\_忽略\_失败**标志。

该驱动程序不需要调用**IWDFIoRequest::Impersonate**它将请求发送到 I/O 目标之前。

如果较低级驱动程序还将转发请求，客户端的模拟级别传输驱动程序堆栈下。

### <a name="reducing-security-threats"></a>减少安全威胁

若要减少"特权提升"受到攻击的可能性，您应该：

-   尽量避免使用模拟。

    例如，若要避免使用模拟打开一个文件，必须将该驱动程序，客户端应用程序可以打开的文件和 I/O 操作用于将文件内容发送到该驱动程序。

-   使用您的驱动程序要求的最低模拟级别。

    设置您的驱动程序 INF 文件中的模拟级别尽可能低。 如果您的驱动程序不需要的任何模拟，不包括**UmdfImpersonationLevel**指令 INF 文件中。

-   最小化攻击者利用您的驱动程序的机会。

    你**OnImpersonate**回调函数应包含执行模拟所需操作的代码的一小部分。 例如，如果您的驱动程序需要访问受保护的文件，它需要模拟仅在打开的文件句柄时。 它不需要模拟以读取或写入到文件。

 

 





