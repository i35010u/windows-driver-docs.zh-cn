---
title: 移植 I/O
description: 移植 I/O
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1988652108b0ce7ec3d99419081160c050c99ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840850"
---
# <a name="porting-io"></a>移植 I/O


KMDF 驱动程序通过创建一个或多个队列，并将一个或多个 i/o 事件回调函数与每个队列关联，来处理 i/o 请求。 将 WDM 驱动程序的 i/o 处理代码移植到 KMDF：

-   [端口 i/o 队列](creating-i-o-queues.md)。

-   [端口 i/o 调度例程](porting-i-o-dispatch-routines-to-i-o-event-callback-functions.md) 到 i/o 事件的回调。

-   [修改处理已完成请求的代码](revise-completed-request-logic.md)。

-   [修订取消的请求逻辑](revise-canceled-request-logic.md)。

-   [修订转发请求逻辑](revise-forward-request-logic.md)。

-   [修订发出 i/o 请求的代码](revise-code-that-issues-i-o-requests.md)。

 

 





