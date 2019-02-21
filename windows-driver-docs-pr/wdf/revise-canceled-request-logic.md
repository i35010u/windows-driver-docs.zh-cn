---
title: 修改已取消的请求逻辑
description: 修改已取消的请求逻辑
ms.assetid: 8246826A-BDBD-4A9B-9FFC-B813033E0FDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16fc56a011372c388de87ca952d5d4b8b9bfd61c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556014"
---
# <a name="revise-canceled-request-logic"></a>修改已取消的请求逻辑


取消 I/O 请求时，WDM 驱动程序必须管理多个困难的争用条件。 在队列中或在驱动程序正在处理时，可能会被取消请求。 在每种情况下，驱动程序必须使用锁的组合以确保它取消并一次完成请求。

WDF 排队机制极大地简化了取消操作。 如果请求已取消在队列上时，该框架将处理取消，而不会通知驱动程序。 该驱动程序可以通过注册请求通知[ *EvtIoCanceledOnQueue* ](https://msdn.microsoft.com/library/windows/hardware/ff541756)回调函数。 该框架已传递到驱动程序的请求后，不是默认情况下可取消请求。 驱动程序可以调用[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)在任何时间，以找出请求已被取消。

有关详细信息，请参阅[取消 I/O 请求](canceling-i-o-requests.md)。

 

 





