---
title: 支持 UMDF 1.x 驱动程序中的内核模式客户端
description: 支持 UMDF 1.x 驱动程序中的内核模式客户端
keywords:
- 内核模式客户端 WDK UMDF
- UMDF 驱动程序 WDK UMDF，内核模式客户端
- 用户模式驱动程序 WDK UMDF、内核模式客户端
- UMDF WDK，内核模式客户端
- User-Mode Driver Framework WDK，内核模式客户端
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a03f3abfba2bec00fdfb5c81e47ae8fe59c2fda7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836617"
---
# <a name="supporting-kernel-mode-clients-in-umdf-1x-drivers"></a>支持 UMDF 1.x 驱动程序中的内核模式客户端

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

>[!WARNING]
>另请参阅 [在 UMDF 2.x 中支持 Kernel-Mode 客户端](supporting-kernel-mode-clients-in-umdf-drivers.md)。

UMDF 版本1.9 及更高版本允许 UMDF 驱动程序支持 *内核模式客户端*。 内核模式客户端可以是以下任一项：

-   位于设备的驱动程序堆栈中的 UMDF 驱动程序之上的内核模式驱动程序。

-   一台设备堆栈的内核模式驱动程序，它支持一台设备，打开另一台设备的句柄，后者设备的驱动程序堆栈包含 UMDF 驱动程序。

换句话说，支持内核模式客户端的 UMDF 驱动程序可以接收来自内核模式驱动程序的 i/o 请求。 内核模式驱动程序可以转发从用户模式应用程序收到的 i/o 请求，也可以创建新的 i/o 请求并将其发送到用户模式驱动程序。

若要确定你的 UMDF 驱动程序是否必须支持内核模式客户端，你必须了解你的驱动程序将添加到的驱动程序堆栈以及你的驱动程序将驻留的位置。 您还必须确定另一个堆栈中的驱动程序是否可以将 i/o 请求发送到您的驱动程序的设备。

如果需要，你的驱动程序必须支持内核模式客户端：

-   内核模式驱动程序可以直接位于驱动程序堆栈中的 UMDF 驱动程序之上。 例如，内核模式筛选器驱动程序可能会直接驻留在基于 UMDF 的函数驱动程序之上。

-   来自另一堆栈的内核模式驱动程序可以将 i/o 请求发送到驱动程序的设备。 例如，你的驱动程序可能会创建一个符号链接，而另一堆栈中的内核模式驱动程序可以使用它来打开驱动程序设备的句柄。 然后，内核模式驱动程序可以将 i/o 请求发送到设备。

### <a name="how-to-support-kernel-mode-clients-in-a-umdf-driver"></a><a href="" id="how-to-support-kernel-mode-clients-in-a-umdf-based-driver"></a>如何在 UMDF 驱动程序中支持内核模式客户端

仅当 UMDF 驱动程序已为内核模式客户端启用支持时，UMDF 驱动程序才能接收来自内核模式驱动程序的 i/o 请求。 此外，如果设备安装尝试将内核模式驱动程序加载到设备的驱动程序堆栈中的 UMDF 驱动程序之上，则该框架仅在 UMDF 驱动程序已启用对内核模式客户端的支持时才会加载驱动程序。

若要为内核模式客户端启用 UMDF 驱动程序支持，UMDF 驱动程序的 INF 文件必须在其 INF *DDInstall* 中包含 [UmdfKernelModeClientPolicy](specifying-wdf-directives-in-inf-files.md)指令。**WDF** 部分。 如果 UMDF 驱动程序的 INF 文件不包括此指令，则 UMDF 不允许运行安装在 UMDF 驱动程序之上的内核模式驱动程序运行。

该框架提供了两种方法，这些方法对支持内核模式客户端的驱动程序很有用。 驱动程序可以调用 [**IWDFIoRequest2：： GetRequestorMode**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-getrequestormode) 方法来确定 i/o 请求是否来自内核模式或用户模式。 如果 i/o 请求来自用户模式，则驱动程序可以调用 [**IWDFIoRequest2：： IsFromUserModeDriver**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-isfromusermodedriver) 来确定请求是来自应用程序还是来自其他用户模式驱动程序。

### <a name="restrictions-on-kernel-mode-drivers"></a>内核模式驱动程序的限制

仅当内核模式驱动程序满足以下要求时，UMDF 驱动程序才能处理来自内核模式驱动程序的 i/o 请求：

-   内核模式驱动程序必须在 \_ 发送 i/o 请求时以 IRQL = 被动级别运行。

-   除非驱动程序已将 **UmdfFileObjectPolicy** INF 指令设置为 **AllowNullAndUnknownFileObjects**，否则内核模式驱动程序发送到用户模式驱动程序的每个 i/o 请求必须具有关联的文件对象。 必须事先通知框架，因为 i/o 管理器已创建文件对象。  (此类通知会导致框架调用用户模式驱动程序的 [**IQueueCallbackCreate：： OnCreateFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile) 回调函数，但该回调函数是可选的。 ) 

-   I/o 请求不能包含 [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md) 函数代码。

-   I/o 请求的缓冲区不得包含指向其他信息的指针，因为用户模式驱动程序无法取消引用指针。

-   如果 i/o 请求包含指定 "两个" 缓冲区访问方法的 [i/o 控制代码](../kernel/introduction-to-i-o-control-codes.md) ，则内核模式驱动程序必须在创建 i/o 请求的应用程序的进程上下文中发送 i/o 请求。 有关如何在 UMDF 基础驱动程序中支持 "两个" 方法的详细信息，请参阅 [在 Umdf 驱动程序中使用非缓冲 i/o 和直接 i/o](./accessing-data-buffers-in-umdf-1-x-drivers.md#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)。

-   UMDF 驱动程序可以在用户模式下修改 i/o 请求的输出数据。 因此，内核模式驱动程序必须验证它从用户模式驱动程序接收到的任何输出数据。

-   通常，内核模式客户端应验证 UMDF 驱动程序传递给 [**IWDFIoRequest：： CompleteWithInformation**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)的 *信息* 值。 如果客户端是 KMDF 驱动程序，它可以调用 [**WdfRequestGetCompletionParams**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams) 以在 IO \_ 状态块结构中获取此信息 \_ 。

    通常情况下，框架不验证 UMDF 驱动程序传递给 [**IWDFIoRequest：： CompleteWithInformation**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)的信息值。  (此参数通常指定传输的字节数。 ) 框架只为输出缓冲区验证信息值，并且仅对 [缓冲的 i/o](./accessing-data-buffers-in-umdf-1-x-drivers.md#using-buffered-i-o-in-umdf-drivers) 数据访问方法进行验证。  (例如，如果访问方法是缓冲 i/o，则框架将验证传输的字节数是否未超过读取操作的输出缓冲区大小。 ) 

### <a name="handling-return-status-values-in-a-umdf-1x-driver"></a><a href="" id="handling-return-status-values"></a>处理 UMDF 1.x 驱动程序中的返回状态值

将返回状态值从用户模式传递到内核模式需要特别注意，如下所示：

-   UMDF 版本1驱动程序通常会接收 HRESULT 类型的返回值，而基于 KMDF 和 WDM 的内核模式驱动程序通常会接收 NTSTATUS 类型的值。 如果为1，则为。*x* 驱动程序完成 i/o 请求，如果驱动程序具有内核模式客户端，则驱动程序对 [**IWDFIoRequest：： Complete**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete) 或 [**IWDFIoRequest：： CompleteWithInformation**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation) 的调用应指定驱动程序从 NTSTATUS 值生成的 HRESULT 值。 通常，为 UMDF 1。*x* 驱动程序应使用 \_ \_ *winerror.h* 中定义的 NT 宏 () 将状态返回到内核模式客户端。 下面的示例演示如何在完成请求时使用此宏。

    ```cpp
    hr = HRESULT_FROM_NT(STATUS_BUFFER_OVERFLOW)
    request->Complete(HRESULT_FROM_NT(STATUS_BUFFER_OVERFLOW);
    return hr;
    ```

    若要将特定的 HRESULT 值返回到内核模式客户端，以下回调必须使用 HRESULT \_ FROM \_ NT 宏：

    -   [**IPnpCallback::OnQueryRemove**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onqueryremove)
    -   [**IPnpCallback::OnQueryStop**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onquerystop)
    -   [**IPnpCallbackHardware::OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)
    -   [**IPnpCallbackHardware::OnReleaseHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)

    若要使用 *ntstatus* 中定义的 ntstatus 值，请使用 UMDF 1。*x* 驱动程序必须包含这两行，然后才能包含任何其他标头。

    ```cpp
    #define UMDF_USING_NTSTATUS
    #include <ntstatus.h>
    ```

    不要使用 HRESULT \_ from \_ NT 宏将状态 SUCCESS 转换为 \_ HRESULT 值。 只需返回 \_ "OK"，如下面的示例中所示。

    ```cpp
    request->Complete(S_OK);
    ```

-   框架代表 UMDF 驱动程序完成一些 i/o 请求。 有时，框架不会将 HRESULT 类型的返回值转换为等效的 NTSTATUS 值，因此框架可能会将 HRESULT 类型的完成状态传递到内核模式客户端。

    由于这种情况，在测试 i/o 请求的完成状态时，内核模式客户端不应使用 NT \_ 错误宏，因为 \_ 对于 HRESULT 错误值，NT 错误宏不会返回 **TRUE** 。 测试 i/o 请求的完成状态时，内核模式驱动程序应使用 NT \_ SUCCESS 宏。

### <a name="kernel-mode-client-support-in-earlier-umdf-versions"></a><a href="" id="kernel-mode-client-support-in-earlier-umdf-versions"></a> 早期 UMDF 版本中的内核模式客户端支持

对于低于版本1.9 的 UMDF 版本，驱动程序的 INF 文件可以包含一个 [**Inf AddReg 指令**](../install/inf-addreg-directive.md)，以在 \_ 设备 [硬件密钥](./using-the-registry-in-umdf-1-x-drivers.md)的 **WUDF** 子项下创建一个 REG DWORD 大小的 **UpperDriverOk** 注册表值。

如果将 **UpperDriverOk** 注册表值设置为非零值，则框架允许将内核模式驱动程序加载到用户模式驱动程序之上。 内核模式驱动程序可以将用户模式应用程序的 i/o 请求转发到 UMDF 驱动程序，但内核模式驱动程序无法将内核模式下创建的 i/o 请求发送到 UMDF 驱动程序。

对于 UMDF 版本1.9 及更高版本， **UpperDriverOk** 注册表值已过时，仅对现有驱动程序提供支持。 新驱动程序应使用 [UmdfKernelModeClientPolicy](specifying-wdf-directives-in-inf-files.md) 指令。

