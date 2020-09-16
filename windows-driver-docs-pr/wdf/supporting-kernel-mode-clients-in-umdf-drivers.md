---
title: 支持 UMDF 驱动程序中的内核模式客户端
description: 本主题介绍用户模式驱动程序框架 (UMDF) 驱动程序如何支持内核模式客户端，从 UMDF 版本2开始。
ms.assetid: 5C0180BF-F0C7-4225-8388-C3315C282516
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48474fba4bd3960716fdb3c98ca195188a80a90a
ms.sourcegitcommit: 9b4760aae390b36dbdf9e0dd729a4a643c3f7831
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90565285"
---
# <a name="supporting-kernel-mode-clients-in-umdf-drivers"></a>支持 UMDF 驱动程序中的内核模式客户端


本主题介绍用户模式驱动程序框架 (UMDF) 驱动程序如何支持 *内核模式客户端*，从 UMDF 版本2开始。

*内核模式的客户端*是一种将 i/o 请求发送到 UMDF 驱动程序的内核模式驱动程序。 内核模式驱动程序可能在 UMDF 驱动程序上、相同的设备堆栈中，或者可能位于不同的设备堆栈中。

内核模式驱动程序可以转发从用户模式应用程序收到的 i/o 请求，也可以创建新的 i/o 请求并将其发送到用户模式驱动程序。

### <a name="how-to-support-kernel-mode-clients-in-a-umdf-driver"></a><a href="" id="how-to-support-kernel-mode-clients-in-a-umdf-based-driver"></a>如何在 UMDF 驱动程序中支持内核模式客户端

若要为内核模式客户端启用 UMDF 驱动程序支持，UMDF 驱动程序的 INF 文件必须在其 INF *DDInstall*中包含[UmdfKernelModeClientPolicy](specifying-wdf-directives-in-inf-files.md)指令。**WDF**部分。

该框架提供了两种方法，这些方法对支持内核模式客户端的驱动程序很有用。 驱动程序可以调用 [**WdfRequestGetRequestorMode**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetrequestormode) 方法来确定 i/o 请求是否来自内核模式或用户模式。 如果 i/o 请求来自用户模式，则驱动程序可以调用 [**WdfRequestIsFromUserModeDriver**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisfromusermodedriver) 来确定请求是来自应用程序还是其他用户模式驱动程序。

### <a name="restrictions-on-kernel-mode-drivers"></a>内核模式驱动程序的限制

仅当内核模式驱动程序满足以下要求时，UMDF 驱动程序才能处理来自内核模式驱动程序的 i/o 请求：

-   内核模式驱动程序必须在 \_ 发送 i/o 请求时以 IRQL = 被动级别运行。

-   除非驱动程序已将 **UmdfFileObjectPolicy** INF 指令设置为 **AllowNullAndUnknownFileObjects**，否则内核模式驱动程序发送到用户模式驱动程序的每个 i/o 请求必须具有关联的文件对象。 必须事先通知框架，因为 i/o 管理器已创建文件对象。  (此类通知会导致框架调用用户模式驱动程序的 [*EvtDeviceFileCreate*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create) 回调函数，但该回调函数是可选的。 ) 

-   I/o 请求不能包含 [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md) 函数代码。

-   I/o 请求的缓冲区不得包含指向其他信息的指针，因为用户模式驱动程序无法取消引用指针。

-   如果 i/o 请求包含指定 "两个" 缓冲区访问方法的 [i/o 控制代码](../kernel/introduction-to-i-o-control-codes.md) ，则内核模式驱动程序必须在创建 i/o 请求的应用程序的进程上下文中发送 i/o 请求。 有关如何在 UMDF 驱动程序中支持 "两个" 方法的详细信息，请参阅 [管理 Umdf 驱动程序中的缓冲区访问方法](managing-buffer-access-methods-in-umdf-drivers.md)。

-   UMDF 驱动程序可以在用户模式下修改 i/o 请求的输出数据。 因此，内核模式驱动程序必须验证它从用户模式驱动程序接收到的任何输出数据。

-   通常，内核模式客户端应验证 UMDF 驱动程序传递给[**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)的*信息*值。 如果客户端是 KMDF 驱动程序，它可以调用 [**WdfRequestGetCompletionParams**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams) 以在 IO \_ 状态块结构中获取此信息 \_ 。

    通常情况下，框架不验证 UMDF 驱动程序传递给 [**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)的信息值。  (此参数通常指定传输的字节数。 ) 框架只为输出缓冲区验证信息值，并且仅对 [缓冲的 i/o](./accessing-data-buffers-in-wdf-drivers.md#direct) 数据访问方法进行验证。  (例如，如果访问方法是缓冲 i/o，则框架将验证传输的字节数是否未超过读取操作的输出缓冲区大小。 ) 

