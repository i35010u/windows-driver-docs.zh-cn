---
title: 使用活动标识符
description: 使用活动标识符
ms.assetid: 2B70953F-5192-4654-9506-6A84373D20B4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d10229f897357f5da9b786d003fbc05d2e28a3b4
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717460"
---
# <a name="using-activity-identifiers"></a>使用活动标识符


在 framework 版本1.11 及更高版本中，UMDF 驱动程序可以设置和检索)  (Id 的活动标识符。 活动 Id 允许你关联多个 i/o 请求，以便你可以使用 Windows 的事件跟踪 (ETW) 跟踪来跟踪它们。 本主题介绍了驱动程序可能使用活动 Id 的一些可能的方案。

## <a name="associating-new-requests-with-an-existing-request"></a>将新请求与现有请求关联


在驱动程序的 i/o 调度回调函数中，可以创建多个框架 i/o 请求，作为传入请求的结果。 驱动程序从原始请求获取活动 ID，并通过调用 [**WdfRequestRetrieveActivityId**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid) 和 [**WdfRequestSetActivityId**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)在新请求中设置该 ID。

有关代码示例，请参阅 [**WdfRequestRetrieveActivityId**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)。

## <a name="associating-new-requests-with-an-existing-thread"></a>将新请求与现有线程关联


驱动程序可能会在非 i/o 调度线程或工作项中创建新的 i/o 请求。 你可以从任何对应的请求中设置此类请求的活动 ID，或使用与 i/o 调度线程关联的活动 ID。 驱动程序可以通过调用 [**EventActivityIdControl**](/windows/win32/api/evntprov/nf-evntprov-eventactivityidcontrol) ，然后调用 [**WdfRequestSetActivityId**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid) 为每个新的 i/o 请求设置标识符，来检索与当前线程关联的活动 ID。

如果驱动程序调用 Win32 API 来发送 i/o 请求，则它可以从原始请求中检索活动 ID，然后将其传播到该线程。 然后，i/o 管理器将与该线程关联的活动 ID 应用到它为响应请求而生成的 (Irp) 的任何 i/o 请求包。

 

