---
title: 支持 UMDF 1.x 驱动程序中的内核模式客户端
description: 支持 UMDF 1.x 驱动程序中的内核模式客户端
ms.assetid: 933dc761-2616-4bee-8357-dbb6644596c2
keywords:
- 内核模式下客户端 WDK UMDF
- UMDF 驱动程序 WDK UMDF，内核模式下客户端
- 用户模式驱动程序 WDK UMDF，内核模式下客户端
- UMDF WDK，内核模式下客户端
- 用户模式驱动程序框架 WDK，内核模式下客户端
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec32535a9052f82d50cc9ba0addba1b932623348
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563541"
---
# <a name="supporting-kernel-mode-clients-in-umdf-1x-drivers"></a>支持 UMDF 1.x 驱动程序中的内核模式客户端

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

>[!WARNING]
>另请参阅[UMDF 中支持内核模式下客户端 2.x](supporting-kernel-mode-clients-in-umdf-drivers.md)。

UMDF 版本 1.9 及更高版本允许 UMDF 驱动程序以支持*内核模式下客户端*。 内核模式下客户端可以是以下之一：

-   承担 UMDF 驱动程序的设备驱动程序堆栈中存在一个内核模式驱动程序。

-   一个支持一台设备，设备堆栈的内核模式驱动程序打开的句柄另一台设备，并且后一种设备的驱动程序堆栈包含 UMDF 驱动程序。

换而言之，UMDF 驱动程序支持的内核模式下客户端可以接收来自内核模式驱动程序的 I/O 请求。 内核模式驱动程序可以将它从用户模式应用程序接收的 I/O 请求转发或可以创建新的 I/O 请求并将其发送到用户模式驱动程序。

若要确定 UMDF 驱动程序必须支持内核模式下客户端，必须了解到将添加您的驱动程序，并在该堆栈中您的驱动程序将驻留的位置的驱动程序堆栈。 您还必须确定从另一个堆栈的驱动程序可能将 I/O 请求发送到您的驱动程序的设备。

如果您的驱动程序必须支持内核模式下客户端：

-   内核模式驱动程序正上方 UMDF 驱动程序在驱动程序堆栈。 例如，内核模式筛选器驱动程序可能位于正上方 UMDF 基于功能驱动程序。

-   从另一个堆栈的内核模式驱动程序可以将 I/O 请求发送到您的驱动程序的设备。 例如，您的驱动程序可能会创建另一个堆栈中的内核模式驱动程序可用来打开您的驱动程序的设备的句柄的符号链接。 内核模式驱动程序然后可以将 I/O 请求发送到设备。

### <a href="" id="how-to-support-kernel-mode-clients-in-a-umdf-based-driver"></a>如何在 UMDF 驱动程序支持内核模式下客户端

只有在 UMDF 驱动程序已启用内核模式下客户端的支持，UMDF 驱动程序可以从内核模式驱动程序接收的 I/O 请求。 此外，如果设备安装尝试加载上面中设备的驱动程序堆栈的 UMDF 驱动程序的内核模式驱动程序，该框架允许驱动程序加载只有在 UMDF 驱动程序已启用内核模式下客户端的支持。

若要启用内核模式下客户端的 UMDF 驱动程序的支持，UMDF 驱动程序的 INF 文件必须包括[UmdfKernelModeClientPolicy](specifying-wdf-directives-in-inf-files.md)指令中其 INF *DDInstall*。**WDF**部分。 如果 UMDF 驱动程序的 INF 文件不包含此指令，UMDF 不允许安装在 UMDF 驱动程序运行的内核模式驱动程序。

该框架提供对支持内核模式下客户端的驱动程序都很有用的两种方法。 驱动程序可以调用[ **IWDFIoRequest2::GetRequestorMode** ](https://msdn.microsoft.com/library/windows/hardware/ff559002)方法来确定的 I/O 请求来自内核模式或用户模式。 如果 I/O 请求来自用户模式下，该驱动程序可以调用[ **IWDFIoRequest2::IsFromUserModeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559021)以确定请求是否来自应用程序或另一个用户模式驱动程序。

### <a name="restrictions-on-kernel-mode-drivers"></a>内核模式驱动程序的限制

UMDF 驱动程序可以处理从内核模式驱动程序的 I/O 请求，仅当内核模式驱动程序符合以下要求：

-   内核模式驱动程序必须运行在 IRQL = 被动\_级别时发送的 I/O 请求。

-   除非已经设置了该驱动程序**UmdfFileObjectPolicy** INF 指令**AllowNullAndUnknownFileObjects**，内核模式驱动程序将发送到的用户模式驱动程序的每个 I/O 请求必须具有一个关联文件对象。 框架必须之前已通知 I/O 管理器创建的文件对象。 (此类通知会导致调用用户模式驱动程序的框架[ **IQueueCallbackCreate::OnCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff556841)回调函数，但回调函数是可选的。)

-   I/O 请求不能包含[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)函数代码。

-   I/O 请求的缓冲区不能包含指向其他信息，因为用户模式驱动程序不能取消引用指针。

-   如果 I/O 请求包含[I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff565406)，它指定"不"缓冲区的访问方法，内核模式驱动程序必须在创建 I/O 请求的应用程序的进程上下文中发送的 I/O 请求。 有关如何在基 UMDF 驱动程序支持"任何"方法的详细信息，请参阅[使用既不缓冲 I/O，也不在 UMDF 驱动程序的直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff554413#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)。

-   UMDF 驱动程序可能会修改在用户模式下的 I/O 请求的输出数据。 因此，内核模式驱动程序必须验证来自用户模式驱动程序收到的任何输出数据。

-   内核模式下客户端通常应验证*信息*UMDF 驱动程序将传递给的值[ **IWDFIoRequest::CompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff559074)。 如果客户端是一个 KMDF 驱动程序，它可以调用[ **WdfRequestGetCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff549961)若要获取此信息在 IO\_状态\_块结构。

    通常情况下，该框架不会验证 UMDF 驱动程序将传递到的信息值[ **IWDFIoRequest::CompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff559074)。 （此参数通常指定传输的字节数。）框架验证信息的值仅用于输出缓冲区，而仅用于[缓冲 I/O](https://msdn.microsoft.com/library/windows/hardware/ff554413#using-buffered-i-o-in-umdf-drivers)数据访问方法。 (例如，框架将验证的传输的字节数不超过的读取操作的输出缓冲区大小是否访问方法进行缓冲处理 I/O。)

### <a href="" id="handling-return-status-values"></a>UMDF 1.x 驱动程序中处理返回状态值

将返回状态的值从用户模式传递到内核模式需要特别注意，如下所示：

-   UMDF 版本 1 的驱动程序通常接收 HRESULT 类型返回值，同时 KMDF 和基于 WDM 的内核模式驱动程序通常接收 NTSTATUS 类型化的值。 如果 UMDF 1。*x*驱动程序完成 I/O 请求，并且如果该驱动程序有一个内核模式下客户端，驱动程序的调用[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)或[ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)应指定驱动程序从 NTSTATUS 值将生成的 HRESULT 值。 通常，UMDF 1。*x*驱动程序应使用 HRESULT\_FROM\_NT 宏 (在中定义*Winerror.h*) 返回到内核模式下客户端的状态。 下面的示例演示如何完成请求时使用此宏。

    ```cpp
    hr = HRESULT_FROM_NT(STATUS_BUFFER_OVERFLOW)
    request->Complete(HRESULT_FROM_NT(STATUS_BUFFER_OVERFLOW);
    return hr;
    ```

    若要将特定的 HRESULT 值返回给内核模式下客户端，以下回调必须使用相应的 HRESULT\_FROM\_NT 宏：

    -   [**IPnpCallback::OnQueryRemove**](https://msdn.microsoft.com/library/windows/hardware/ff556808)
    -   [**IPnpCallback::OnQueryStop**](https://msdn.microsoft.com/library/windows/hardware/ff556811)
    -   [**IPnpCallbackHardware::OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556766)
    -   [**IPnpCallbackHardware::OnReleaseHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556768)

    若要使用的定义中的 NTSTATUS 值*ntstatus.h*，UMDF 1。*x*包含任何其他标头之前，驱动程序必须包含以下两行。

    ```cpp
    #define UMDF_USING_NTSTATUS
    #include <ntstatus.h>
    ```

    不使用 HRESULT\_FROM\_NT 宏将转换状态\_成功从 NTSTATUS 值为 HRESULT 值。 只需返回 S\_好了，如下面的示例中所示。

    ```cpp
    request->Complete(S_OK);
    ```

-   由框架完成一些代表 UMDF 驱动程序的 I/O 请求。 有时框架不会转换为 HRESULT 类型返回值等效的 NTSTATUS 值，因此框架可能会将 HRESULT 类型完成状态传递到内核模式下客户端。

    由于这种情况下，内核模式下客户端不应使用 NT\_错误宏时测试的 I/O 请求的完成状态，因为 NT\_不会返回错误宏**TRUE** HRESULT 错误值。 内核模式驱动程序应使用 NT\_成功宏测试 I/O 请求的完成状态时。

### <a href="" id="kernel-mode-client-support-in-earlier-umdf-versions"></a> 在早期 UMDF 版本中的内核模式下客户端支持

对于 UMDF 版本早于版本 1.9，驱动程序的 INF 文件可以包括[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)若要创建的 REG\_尺寸 DWORD **UpperDriverOk**下的注册表值**WUDF**的设备的子项[硬件密钥](https://msdn.microsoft.com/library/windows/hardware/ff561381)。

如果**UpperDriverOk**注册表值设置为非零数字，该框架允许要在用户模式驱动程序加载的内核模式驱动程序。 内核模式驱动程序可以将 I/O 请求转发从用户模式应用程序到 UMDF 驱动程序，但内核模式驱动程序不能发送在 UMDF 驱动程序的内核模式下创建的 I/O 请求。

对于 UMDF 版本 1.9 及更高版本， **UpperDriverOk**注册表值已过时，仅对现有的驱动程序的受支持。 新的驱动程序应使用[UmdfKernelModeClientPolicy](specifying-wdf-directives-in-inf-files.md)指令。

 

 





