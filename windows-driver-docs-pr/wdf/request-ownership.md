---
title: 请求所有权
description: 请求所有权
keywords:
- 请求对象 WDK KMDF，所有权
- 所有权 WDK KMDF、i/o 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 914a594d83c86c5e35b2855c36d128b98a9fb738
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821709"
---
# <a name="request-ownership"></a>请求所有权


当 i/o 管理器将 i/o 请求发送到基于框架的驱动程序时，框架会截获请求并创建框架请求对象。 由于只有框架可以访问请求并对对象执行操作，因此框架 "拥有" 请求对象。

在框架创建请求对象后，它会将该对象置于某个驱动程序的 i/o 队列中。 框架将继续拥有请求对象，直到它从队列中删除该请求并将其传递给驱动程序。

驱动程序 [收到](receiving-i-o-requests.md) 请求对象后，它将拥有该请求。 驱动程序可以通过句柄访问请求对象，并对对象执行操作。 尽管驱动程序拥有请求对象，但它可以 [重新排队](requeuing-i-o-requests.md)、 [完成](completing-i-o-requests.md)、 [取消](canceling-i-o-requests.md)或 [转发](forwarding-i-o-requests.md) 请求，之后它不再拥有请求对象并且无法访问。

由于请求对象的所有权在驱动程序和框架之间传递，因此对象句柄的值不会更改。 例如，如果驱动程序收到来自 i/o 队列的请求，请将其会到不同的队列，然后再次收到请求，句柄的值将不会更改。 同样，如果驱动程序将请求转发到 i/o 目标，并在以后收到 i/o 目标完成请求的通知，则驱动程序的通知回调函数将接收驱动程序提供给 i/o 目标的相同句柄值。

 

 





