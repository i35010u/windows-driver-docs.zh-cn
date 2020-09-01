---
title: 修改已取消的请求逻辑
description: 修改已取消的请求逻辑
ms.assetid: 8246826A-BDBD-4A9B-9FFC-B813033E0FDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 688a6eb7499507215b6978004873e2d756b82de1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189663"
---
# <a name="revise-canceled-request-logic"></a>修改已取消的请求逻辑


当 i/o 请求被取消时，WDM 驱动程序必须管理几个困难的争用情况。 当请求在队列中或当驱动程序正在处理请求时，可能会取消该请求。 在每种情况下，驱动程序都必须使用锁的组合，以确保它仅取消并完成请求一次。

WDF 队列机制可大大简化取消。 如果请求在队列中被取消，则框架将在不通知驱动程序的情况下处理取消。 驱动程序可以通过注册 [*EvtIoCanceledOnQueue*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue) 回调函数来请求通知。 框架将请求传递给驱动程序后，默认情况下不能取消该请求。 驱动程序可以随时调用 [**WdfRequestIsCanceled**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled) ，以确定是否已取消请求。

有关详细信息，请参阅 [取消 I/o 请求](canceling-i-o-requests.md)。

 

