---
title: 使用活动标识符
description: 使用活动标识符
ms.assetid: 2B70953F-5192-4654-9506-6A84373D20B4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09ca53f29d2e8e761ac7851f8695f4d4249806fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372282"
---
# <a name="using-activity-identifiers"></a>使用活动标识符


1\.11 及更高版本的 framework 版本，在 UMDF 驱动程序可以设置和检索活动标识符 (Id)。 活动 Id，可将多个 I/O 请求，相关联，以便可以跟踪其使用 Windows 事件跟踪 (ETW) 跟踪。 本主题介绍一些可能的方案，该驱动程序可能使用活动 Id。

## <a name="associating-new-requests-with-an-existing-request"></a>将新的请求与现有的请求相关联


在您的驱动程序的 I/O 调度回调函数中，您可以创建多个框架 I/O 请求传入请求的结果。 该驱动程序从原始请求获取活动 ID，并通过调用来设置新的请求中[ **WdfRequestRetrieveActivityId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)并[ **WdfRequestSetActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)。

有关代码示例，请参阅[ **WdfRequestRetrieveActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)。

## <a name="associating-new-requests-with-an-existing-thread"></a>将新请求关联的现有线程


在 I/O 调度线程，以外的线程或工作项中，驱动程序可能会创建新的 I/O 请求。 从任何相应的请求，或通过使用与 I/O 调度线程关联的活动 ID，可以设置此类请求的活动 ID。 该驱动程序可以检索通过调用与当前线程关联的活动 ID [ **EventActivityIdControl** ](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol) ，然后再调用[ **WdfRequestSetActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)可设置为每个新的 I/O 请求的标识符。

如果驱动程序调用 Win32 API 发送的 I/O 请求时，它可以从原始请求中检索活动 ID 并将其传播到该线程。 然后，I/O 管理器应用到它在对请求响应中生成任何 I/O 请求数据包 (Irp) 线程与相关联的活动 ID。

 

 





