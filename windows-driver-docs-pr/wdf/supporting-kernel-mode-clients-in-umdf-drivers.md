---
title: 支持 UMDF 驱动程序中的内核模式客户端
description: 本主题介绍用户模式驱动程序框架（UMDF）驱动程序如何支持内核模式客户端，从 UMDF 版本2开始。
ms.assetid: 5C0180BF-F0C7-4225-8388-C3315C282516
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a4f309a5f9f1f902de04fa300538f01ac660921
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831764"
---
# <a name="supporting-kernel-mode-clients-in-umdf-drivers"></a>支持 UMDF 驱动程序中的内核模式客户端


本主题介绍用户模式驱动程序框架（UMDF）驱动程序如何支持*内核模式客户端*，从 UMDF 版本2开始。

*内核模式的客户端*是一种将 i/o 请求发送到 UMDF 驱动程序的内核模式驱动程序。 内核模式驱动程序可能在 UMDF 驱动程序上、相同的设备堆栈中，或者可能位于不同的设备堆栈中。

内核模式驱动程序可以转发从用户模式应用程序收到的 i/o 请求，也可以创建新的 i/o 请求并将其发送到用户模式驱动程序。

### <a href="" id="how-to-support-kernel-mode-clients-in-a-umdf-based-driver"></a>如何在 UMDF 驱动程序中支持内核模式客户端

若要为内核模式客户端启用 UMDF 驱动程序支持，UMDF 驱动程序的 INF 文件必须在其 INF *DDInstall*中包含[UmdfKernelModeClientPolicy](specifying-wdf-directives-in-inf-files.md)指令。**WDF**部分。

该框架提供了两种方法，这些方法对支持内核模式客户端的驱动程序很有用。 驱动程序可以调用[**WdfRequestGetRequestorMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetrequestormode)方法来确定 i/o 请求是否来自内核模式或用户模式。 如果 i/o 请求来自用户模式，则驱动程序可以调用[**WdfRequestIsFromUserModeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisfromusermodedriver)来确定请求是来自应用程序还是其他用户模式驱动程序。

### <a name="restrictions-on-kernel-mode-drivers"></a>内核模式驱动程序的限制

仅当内核模式驱动程序满足以下要求时，UMDF 驱动程序才能处理来自内核模式驱动程序的 i/o 请求：

-   内核模式驱动程序必须在发送 i/o 请求时以 IRQL = 被动\_级别运行。

-   除非驱动程序已将**UmdfFileObjectPolicy** INF 指令设置为**AllowNullAndUnknownFileObjects**，否则内核模式驱动程序发送到用户模式驱动程序的每个 i/o 请求必须具有关联的文件对象。 必须事先通知框架，因为 i/o 管理器已创建文件对象。 （此类通知会导致框架调用用户模式驱动程序的[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调函数，但该回调函数是可选的。）

-   I/o 请求不能包含[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)函数代码。

-   I/o 请求的缓冲区不得包含指向其他信息的指针，因为用户模式驱动程序无法取消引用指针。

-   如果 i/o 请求包含指定 "两个" 缓冲区访问方法的[i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)，则内核模式驱动程序必须在创建 i/o 请求的应用程序的进程上下文中发送 i/o 请求。 有关如何在 UMDF 驱动程序中支持 "两个" 方法的详细信息，请参阅[管理 Umdf 驱动程序中的缓冲区访问方法](managing-buffer-access-methods-in-umdf-drivers.md)。

-   UMDF 驱动程序可以在用户模式下修改 i/o 请求的输出数据。 因此，内核模式驱动程序必须验证它从用户模式驱动程序接收到的任何输出数据。

-   通常，内核模式客户端应验证 UMDF 驱动程序传递给[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)的*信息*值。 如果客户端是 KMDF 驱动程序，则它可以调用[**WdfRequestGetCompletionParams**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)以在 IO\_状态\_块结构中获取此信息。

    通常情况下，框架不验证 UMDF 驱动程序传递给[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)的信息值。 （此参数通常指定传输的字节数。）此框架仅验证输出缓冲区的信息值，并且仅验证[缓冲 i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#direct)数据访问方法的信息值。 （例如，如果访问方法为缓冲 i/o，则框架将验证传输的字节数是否未超过读取操作的输出缓冲区大小。）

 

 





