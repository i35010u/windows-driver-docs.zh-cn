---
title: 完成 I/O 请求
description: 完成 I/O 请求
ms.assetid: ec5aef7a-110e-430c-902d-669ccc7095ac
keywords:
- I/o 请求 WDK KMDF，完成
- 完成 i/o 请求 WDK KMDF
- 请求处理 WDK KMDF，完成请求
- 状态信息 WDK KMDF，完成 i/o 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 778a52af7323c6968a93da2fc3ab6c6f5c17a74a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843648"
---
# <a name="completing-io-requests"></a>完成 I/O 请求





每个基于框架的驱动程序都必须最终完成从框架接收的每个 i/o 请求。 驱动程序通过调用请求对象的[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)或[**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)方法来完成请求。

### <a name="when-to-complete-a-request"></a>何时完成请求

当驱动程序确定下列情况之一为真时，驱动程序必须完成请求：

-   请求的 i/o 操作已成功完成。

-   请求的 i/o 操作已启动，但在完成之前失败。

-   请求的 i/o 操作不受支持，或在收到该操作时无效，无法启动。

-   已取消请求的 i/o 操作。

如果驱动程序通过在设备上创建 i/o 活动来服务 i/o 请求，驱动程序通常会从其[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 。

如果驱动程序收到不受支持或无效的请求，通常会从收到请求的[请求处理程序](request-handlers.md)中调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 。

如果已[取消](canceling-i-o-requests.md)i/o 操作，驱动程序通常会从其[*EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 。

如果驱动程序将 i/o 请求[转发](forwarding-i-o-requests.md)到[i/o 目标](using-i-o-targets.md)，则驱动程序将在 i/o 目标完成请求之后完成请求，如下所示：

-   如果你的驱动程序以[同步](sending-i-o-requests-synchronously.md)方式将 i/o 请求转发到 i/o 目标，则仅在较低级别的驱动程序完成该请求后，才会返回驱动程序对 i/o 目标的调用（除非发生错误）。 I/o 目标返回后，你的驱动程序必须调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)。

-   如果你的驱动程序以[异步方式](sending-i-o-requests-asynchronously.md)转发 i/o 请求，则你将希望在较低级别的驱动程序完成请求时通知你的驱动程序。 如果驱动程序注册了一个[*CompletionRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数，则在 i/o 目标完成该请求后，框架将调用此回调函数。 *CompletionRoutine*回调函数通常会调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)。

若要注册[*CompletionRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数，驱动程序必须先调用[**WdfRequestSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine) ，然后再将 i/o 请求转发到 i/o 目标。

如果在 i/o 目标完成异步转发的 i/o 请求时，驱动程序无需收到通知，则驱动程序无需注册[*CompletionRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数。 相反，在调用[**WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)时，驱动程序可以设置[**WDF\_请求\_发送\_选项\_发送\_并\_忘记**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags)标志。 在这种情况下，驱动程序不会调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)。

驱动程序不会完成通过调用[**WdfRequestCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)或[**WdfRequestCreateFromIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)创建的 i/o 请求。 相反，驱动程序必须调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)来删除请求对象，通常是在 i/o 目标完成请求后。

例如，对于大于驱动程序的 i/o 目标可以一次处理的数据量，驱动程序可能会收到读取或写入请求。 驱动程序必须将数据分成几个较小的请求，并将这些较小的请求发送到一个或多个 i/o 目标。 用于处理这种情况的方法包括：

-   调用[**WdfRequestCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)可创建一个表示小型请求的其他请求对象。

    驱动程序可以将此请求同步发送到 i/o 目标。 较小的请求的[*CompletionRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数可以调用[**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse) ，以便驱动程序可以重用该请求并再次将其发送到 i/o 目标。 在 i/o 目标完成最后一个较小的请求后， *CompletionRoutine*回调函数可以调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)来删除驱动程序创建的请求对象，驱动程序可以调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成原始请求。

-   调用[**WdfRequestCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)可创建多个表示较小请求的其他请求对象。

    驱动程序的 i/o 目标可以异步处理多个较小的请求。 驱动程序可以为每个较小的请求注册一个[*CompletionRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数。 每次调用*CompletionRoutine*回调函数时，它都可以调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)来删除驱动程序创建的请求对象。 在 i/o 目标完成所有较小的请求之后，驱动程序可以调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成原始请求。

### <a href="" id="providing-completion-information"></a>提供完成信息

当驱动程序完成请求时，它可以根据需要提供其他驱动程序可以访问的其他信息。 例如，驱动程序可能提供为读取或写入请求传输的字节数。 为提供此信息，驱动程序可以执行以下任一操作：

-   在调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)之前调用[**WdfRequestSetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetinformation) 。

-   调用[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)。

### <a href="" id="obtaining-completion-information"></a>获取完成信息

若要获取有关另一驱动程序已完成的 i/o 请求的信息，驱动程序可以：

-   调用[**WdfRequestGetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetstatus)可获取低级驱动程序在调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)时指定的完成状态值。

-   调用[**WdfRequestGetCompletionParams**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)可获取[**WDF\_请求\_完成\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_completion_params)结构，其中包含有关已完成请求的附加信息（例如，表示请求的缓冲区或特定于总线的信息。

    仅当驱动程序调用[**WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)以同步或异步方式将 i/o 请求发送到 i/o 目标后，才能调用[**WdfRequestGetCompletionParams**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams) 。 驱动程序在调用将 i/o 请求发送到 i/o 目标的方法之一（如[**WdfIoTargetSendReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)）后，不能调用**WdfRequestGetCompletionParams** 。

-   如果驱动程序中的驱动程序的驱动程序中的驱动程序，请调用[**WdfRequestGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetinformation)来获取更低级别的驱动程序在调用[**WdfRequestSetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetinformation)或[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)时指定stack 提供此类信息。

如果驱动程序同步发送 i/o 请求，则它通常在同步调用返回后调用[**WdfRequestGetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetstatus)、 [**WdfRequestGetCompletionParams**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)和[**WdfRequestGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetinformation) 。 如果驱动程序以异步方式发送 i/o 请求，则通常从[*CompletionRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数中调用这些方法。

有关完成 i/o 请求的详细信息，请参阅[同步取消和完成代码](synchronizing-cancel-and-completion-code.md)。

 

 





