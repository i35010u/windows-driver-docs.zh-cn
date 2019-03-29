---
title: 请求所有权
description: 请求所有权
ms.assetid: 60494e97-0483-454f-aafc-7a69019c95f2
keywords:
- 请求对象 WDK KMDF，所有权
- 所有权 WDK KMDF，I/O 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30885d929be0f951588069a7b951974eecce39ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569492"
---
# <a name="request-ownership"></a>请求所有权


当 I/O 管理器将 I/O 请求发送到基于 framework 的驱动程序时，框架将截获的请求，并创建一个框架请求对象。 框架"拥有"请求对象，因为仅 framework 可以访问请求，并针对对象执行操作。

框架将创建一个请求对象后，它会将一个驱动程序的 I/O 队列中的对象。 框架将继续拥有请求对象，直到将它从队列中移除该请求并将其传递给驱动程序。

该驱动程序后[接收](receiving-i-o-requests.md)请求对象，它将拥有该请求。 该驱动程序可以通过一个句柄访问请求对象并执行对象上的操作。 该驱动程序拥有的请求对象时它可以[重新排队](requeuing-i-o-requests.md)，[完整](completing-i-o-requests.md)，[取消](canceling-i-o-requests.md)，或[向前](forwarding-i-o-requests.md)后它不能再请求拥有请求对象，并且不能访问它。

驱动程序和框架之间传递请求对象的所有权，则不会更改对象句柄的值。 例如，如果驱动程序收到来自 I/O 队列的请求，请求到不同的队列，然后再次接收请求，该句柄的值不会更改。 同样，如果驱动程序将请求转发到 I/O 目标并在稍后接收 I/O 目标已完成请求的通知，驱动程序的通知回调函数接收相同驱动程序提供给 I/O 目标的句柄值。

 

 





