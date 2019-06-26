---
title: 修改已取消的请求逻辑
description: 修改已取消的请求逻辑
ms.assetid: 8246826A-BDBD-4A9B-9FFC-B813033E0FDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4ea240da4298cdf810d3d7c9de5f1b0edded90c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376251"
---
# <a name="revise-canceled-request-logic"></a>修改已取消的请求逻辑


取消 I/O 请求时，WDM 驱动程序必须管理多个困难的争用条件。 在队列中或在驱动程序正在处理时，可能会被取消请求。 在每种情况下，驱动程序必须使用锁的组合以确保它取消并一次完成请求。

WDF 排队机制极大地简化了取消操作。 如果请求已取消在队列上时，该框架将处理取消，而不会通知驱动程序。 该驱动程序可以通过注册请求通知[ *EvtIoCanceledOnQueue* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)回调函数。 该框架已传递到驱动程序的请求后，不是默认情况下可取消请求。 驱动程序可以调用[ **WdfRequestIsCanceled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)在任何时间，以找出请求已被取消。

有关详细信息，请参阅[取消 I/O 请求](canceling-i-o-requests.md)。

 

 





