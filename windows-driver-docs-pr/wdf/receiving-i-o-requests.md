---
title: 接收 I/O 请求
description: 接收 I/O 请求
keywords:
- I/o 请求 WDK KMDF，接收
- 正在接收 i/o 请求 WDK KMDF
- 请求处理 WDK KMDF，接收请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c19c3e32d270aff5ef3879e20b2f90c015f81754
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825297"
---
# <a name="receiving-io-requests"></a>接收 I/O 请求


如果基于框架的驱动程序对 i/o 队列使用了 [顺序](dispatching-methods-for-i-o-requests.md#sequential-dispatching) 或 [并行](dispatching-methods-for-i-o-requests.md#parallel-dispatching) 调度方法，则它会将队列中的 i/o 请求作为输入参数接收到其 [请求处理程序](request-handlers.md)。

如果基于框架的驱动程序使用 i/o 队列的 [手动](dispatching-methods-for-i-o-requests.md#manual-dispatching) 调度方法，则它会通过轮询队列来从队列中获取 i/o 请求。

驱动程序收到请求后，它将 [拥有](request-ownership.md) 请求，直到它 [会](requeuing-i-o-requests.md)、 [完成](completing-i-o-requests.md)、 [取消](canceling-i-o-requests.md)或 [转发](forwarding-i-o-requests.md) 请求。

 

 





