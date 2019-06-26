---
title: 支持 UMDF 驱动程序中的内核模式客户端
description: 本主题介绍用户模式驱动程序框架 (UMDF) 驱动程序如何支持内核模式客户端，在 UMDF 版本 2 中启动。
ms.assetid: 5C0180BF-F0C7-4225-8388-C3315C282516
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f07439199ff0d88df69d6a6736181baaa1c1597
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368084"
---
# <a name="supporting-kernel-mode-clients-in-umdf-drivers"></a>支持 UMDF 驱动程序中的内核模式客户端


本主题介绍用户模式驱动程序框架 (UMDF) 驱动程序如何支持*内核模式下客户端*，从在 UMDF 版本 2 开始。

一个*内核模式下客户端*是将输入/输出请求发送到 UMDF 驱动程序的内核模式驱动程序。 内核模式驱动程序可能会高于 UMDF 驱动程序，在同一个设备堆栈，也可能是不同设备堆栈中。

内核模式驱动程序可以将它从用户模式应用程序接收的 I/O 请求转发或可以创建新的 I/O 请求并将其发送到用户模式驱动程序。

### <a href="" id="how-to-support-kernel-mode-clients-in-a-umdf-based-driver"></a>如何在 UMDF 驱动程序支持内核模式下客户端

若要启用内核模式下客户端的 UMDF 驱动程序的支持，UMDF 驱动程序的 INF 文件必须包括[UmdfKernelModeClientPolicy](specifying-wdf-directives-in-inf-files.md)指令中其 INF *DDInstall*。**WDF**部分。

该框架提供对支持内核模式下客户端的驱动程序都很有用的两种方法。 驱动程序可以调用[ **WdfRequestGetRequestorMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetrequestormode)方法来确定的 I/O 请求来自内核模式或用户模式。 如果 I/O 请求来自用户模式下，该驱动程序可以调用[ **WdfRequestIsFromUserModeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestisfromusermodedriver)以确定请求是否来自应用程序或另一个用户模式驱动程序。

### <a name="restrictions-on-kernel-mode-drivers"></a>内核模式驱动程序的限制

UMDF 驱动程序可以处理从内核模式驱动程序的 I/O 请求，仅当内核模式驱动程序符合以下要求：

-   内核模式驱动程序必须运行在 IRQL = 被动\_级别时发送的 I/O 请求。

-   除非已经设置了该驱动程序**UmdfFileObjectPolicy** INF 指令**AllowNullAndUnknownFileObjects**，内核模式驱动程序将发送到的用户模式驱动程序的每个 I/O 请求必须具有一个关联文件对象。 框架必须之前已通知 I/O 管理器创建的文件对象。 (此类通知会导致调用用户模式驱动程序的框架[ *EvtDeviceFileCreate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调函数，但回调函数是可选的。)

-   I/O 请求不能包含[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)函数代码。

-   I/O 请求的缓冲区不能包含指向其他信息，因为用户模式驱动程序不能取消引用指针。

-   如果 I/O 请求包含[I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)，它指定"不"缓冲区的访问方法，内核模式驱动程序必须在创建 I/O 请求的应用程序的进程上下文中发送的 I/O 请求。 有关如何在 UMDF 驱动程序支持"任何"方法的详细信息，请参阅[UMDF 驱动程序中管理缓冲区的访问方法](managing-buffer-access-methods-in-umdf-drivers.md)。

-   UMDF 驱动程序可能会修改在用户模式下的 I/O 请求的输出数据。 因此，内核模式驱动程序必须验证来自用户模式驱动程序收到的任何输出数据。

-   内核模式下客户端通常应验证*信息*UMDF 驱动程序将传递给的值[ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)。 如果客户端是一个 KMDF 驱动程序，它可以调用[ **WdfRequestGetCompletionParams** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)若要获取此信息在 IO\_状态\_块结构。

    通常情况下，该框架不会验证 UMDF 驱动程序将传递到的信息值[ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)。 （此参数通常指定传输的字节数。）框架验证信息的值仅用于输出缓冲区，而仅用于[缓冲 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#direct)数据访问方法。 (例如，框架将验证的传输的字节数不超过的读取操作的输出缓冲区大小是否访问方法进行缓冲处理 I/O。)

 

 





