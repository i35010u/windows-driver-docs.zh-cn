---
title: 处理 UMDF 1.x 驱动程序中的客户端模拟
description: 处理 UMDF 1.x 驱动程序中的客户端模拟
keywords:
- User-Mode Driver Framework WDK，模拟
- UMDF WDK，模拟
- 用户模式驱动程序 WDK UMDF、模拟
- 模拟 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d96a73129a87164c74aeae99d355becdcea3ef3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814751"
---
# <a name="handling-client-impersonation-in-umdf-1x-drivers"></a>处理 UMDF 1.x 驱动程序中的客户端模拟


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

UMDF 驱动程序通常在 LocalService 帐户下运行，并且无法访问需要用户凭据的文件或资源，如受保护的文件或其他受保护的资源。 UMDF 驱动程序通常对在客户端应用程序和设备之间流动的命令和数据进行操作。 因此，大多数 UMDF 驱动程序不会访问受保护的资源。

但是，某些驱动程序可能需要访问受保护的资源。 例如，UMDF 驱动程序可以通过客户端应用程序提供的文件将固件加载到设备。 此文件可能有 (ACL) 的访问控制列表，该列表可阻止未经授权的用户修改文件和控制设备。 遗憾的是，此 ACL 还会阻止 UMDF 驱动程序访问该文件。

该框架提供了一种模拟功能，该功能允许驱动程序模拟驱动程序的客户端，并获取客户端对受保护资源的访问权限。

### <a name="enabling-impersonation"></a>启用模拟

UMDF 驱动程序的安装包和客户端应用程序必须启用框架的模拟功能，如下所示：

-   UMDF 驱动程序的安装包的 INF 文件必须包含 **UmdfImpersonationLevel** 指令并设置允许的最大模拟级别。 仅当 INF 文件包含 **UmdfImpersonationLevel** 指令时，才启用模拟。 有关设置模拟级别的详细信息，请参阅 [在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

-   客户端应用程序必须为每个文件句柄设置允许的模拟级别。 应用程序使用 Microsoft Win32 **CreateFile** 函数中的服务质量 (QoS) 设置来设置允许的模拟级别。 有关这些设置的详细信息，请参阅 Windows SDK 文档中的 **CreateFile** 的 *dwFlagsAndAttributes* 参数。

### <a name="handling-impersonation-for-an-io-request"></a>处理 i/o 请求的模拟

UMDF 驱动程序和框架按以下顺序处理 i/o 请求的模拟：

1.  驱动程序调用 [**IWDFIoRequest：：模拟**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-impersonate) 方法以指定所需的模拟级别和 [**IImpersonateCallback：： OnImpersonate**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iimpersonatecallback-onimpersonate) 回调函数。

2.  框架检查请求的模拟级别。 如果请求的级别大于 UMDF 驱动程序的安装包和客户端应用程序允许的级别，则模拟请求会失败。 否则，框架将模拟客户端，并立即调用 **OnImpersonate** 回调函数。

**OnImpersonate** 回调函数必须只执行需要请求的模拟级别的操作，例如打开受保护的文件。

UMDF 不允许驱动程序的 **OnImpersonate** 回调函数调用框架的任何对象方法。 这可确保驱动程序不会向其他驱动程序回调函数或其他驱动程序公开模拟级别。

**注意**   在 UMDF 版本1.0 到1.7 中， [**IWDFIoRequest：：模拟**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-impersonate) 授予客户端应用程序和 INF 文件允许的最高模拟级别，即使驱动程序请求的模拟级别较低。 在 UMFD 版本1.9 及更高版本中， **模拟** 方法仅授予驱动程序请求的模拟级别。

 

### <a name="passing-credentials-down-the-driver-stack"></a>沿驱动程序堆栈向下传递凭据

当你的驱动程序收到 [**WdfRequestCreate**](/windows-hardware/drivers/ddi/wudfddi_types/ne-wudfddi_types-_wdf_request_type)类型的 i/o 请求时，驱动程序可能会将该驱动程序堆栈向下移动 i/o 请求。 内核模式驱动程序没有模拟功能， **IWDFIoRequest：：模拟** 可提供给基于 UMDF 的驱动程序。

因此，如果您希望内核模式驱动程序接收客户端的用户凭据 (而不是 [驱动程序主机进程](umdf-driver-host-process.md)的凭据) ，则在调用 [**IWDFIoRequest：： send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)将 create 请求发送到 i/o 目标时，驱动程序必须设置 [**WDF \_ 请求 \_ 发送 \_ 选项 \_ 模拟 \_ 客户端**](/windows-hardware/drivers/ddi/wudfddi_types/ne-wudfddi_types-_wdf_request_send_options_flags)标志。 如果模拟尝试失败， **Send** 方法将返回错误代码，除非驱动程序还设置 **WDF \_ 请求 \_ 发送选项 " \_ \_ 模拟 \_ 忽略 \_ 失败** 标志"。

在向 i/o 目标发送请求之前，驱动程序不必调用 **IWDFIoRequest：：模拟** 。

如果低级驱动程序还转发请求，客户端的模拟级别会沿着驱动程序堆栈向下传递。

### <a name="reducing-security-threats"></a>降低安全威胁

为了降低 "特权提升" 攻击的几率，你应该：

-   尝试避免使用模拟。

    例如，若要避免使用模拟打开驱动程序必须使用的文件，客户端应用程序可以打开该文件，并使用 i/o 操作将文件内容发送到该驱动程序。

-   使用驱动程序所需的最低模拟级别。

    将驱动程序的 INF 文件中的模拟级别设置为尽可能低。 如果你的驱动程序不需要任何模拟，请不要在 INF 文件中包含 **UmdfImpersonationLevel** 指令。

-   最大程度地减少攻击者利用驱动程序的机会。

    **OnImpersonate** 回调函数应包含一小部分代码，仅执行需要模拟的操作。 例如，如果您的驱动程序访问受保护的文件，则它仅在打开文件句柄时才需要模拟。 它不需要模拟即可读取或写入文件。

 

