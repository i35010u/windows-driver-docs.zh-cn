---
title: 接收 I/O 请求
description: 接收 I/O 请求
ms.assetid: 0bd41b7b-d64e-4d02-ab5c-0188e926c8e1
keywords:
- I/O 请求 WDK KMDF，接收
- 接收 I/O 请求 WDK KMDF
- 请求处理 WDK KMDF、 接收的请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a1f53df10d9195dffb0c2821816aed56ad5fd27
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564702"
---
# <a name="receiving-io-requests"></a>接收 I/O 请求


如果使用基于 framework 的驱动程序[顺序](dispatching-methods-for-i-o-requests.md#sequential-dispatching)或[并行](dispatching-methods-for-i-o-requests.md#parallel-dispatching)调度 I/O 队列的方法，它 I/O 请求从队列接收到输入参数作为其[请求处理程序](request-handlers.md).

如果使用基于 framework 的驱动程序[手动](dispatching-methods-for-i-o-requests.md#manual-dispatching)调度 I/O 队列的方法，它获取的 I/O 请求从队列轮询队列。

该驱动程序收到请求时之后, 它[拥有](request-ownership.md)直至其请求[requeues](requeuing-i-o-requests.md)，[完成](completing-i-o-requests.md)，[取消](canceling-i-o-requests.md)，或[将转发](forwarding-i-o-requests.md)请求。

 

 





