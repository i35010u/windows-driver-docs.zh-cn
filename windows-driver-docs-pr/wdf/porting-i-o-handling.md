---
title: 移植 I/O
description: 移植 I/O
ms.assetid: D65B85C4-401F-4143-9626-5C16E24925A0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a991b3a73d9014e3214c5409869973c238a3de43
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390096"
---
# <a name="porting-io"></a>移植 I/O


KMDF 驱动程序通过创建一个或多个队列并将一个或多个 I/O 事件回调函数关联与每个队列处理 I/O 请求。 若要移植 WDM 驱动程序的 I/O 处理代码，KMDF:

-   [端口 I/O 队列](creating-i-o-queues.md)。

-   [端口 I/O 调度例程](porting-i-o-dispatch-routines-to-i-o-event-callback-functions.md)到 I/O 事件的回调。

-   [修改代码，以便处理已完成请求](revise-completed-request-logic.md)。

-   [修改已取消请求逻辑](revise-canceled-request-logic.md)。

-   [修改转发请求逻辑](revise-forward-request-logic.md)。

-   [修改代码发出 I/O 请求](revise-code-that-issues-i-o-requests.md)。

 

 





