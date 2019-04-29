---
title: 处理协议驱动程序中的 PnP 事件通知
description: 处理协议驱动程序中的 PnP 事件通知
ms.assetid: 7c6c9bc5-37ce-49f4-8e39-5f51a266836a
keywords:
- 即插即用 WDK NDIS 协议
- 通知 WDK 即插即用，协议的 NDIS 驱动程序
- 事件通知 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a9478641ead2a01c402b12e4e549052b56ea40b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322274"
---
# <a name="handling-pnp-event-notifications-in-a-protocol-driver"></a>处理协议驱动程序中的 PnP 事件通知





NDIS 6.0 和更高版本的协议驱动程序处理同一插即用 (PnP) 事件通知作为除了到 NDIS 6.0 及更高版本特定的事件通知的 NDIS 5.x 驱动程序。 即插即用事件通知的处理是特定的驱动程序。

若要通知网络即插即用事件协议驱动程序，NDIS 调用驱动程序的[ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)函数。 若要定义的事件的事件类型和特征，NDIS 传递[ **NET\_PNP\_事件\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff568752)结构在*NetPnPEvent*的事件参数*ProtocolNetPnPEvent*。

协议驱动程序应处理驱动程序堆栈的更改。 有关驱动程序堆栈更改的详细信息，请参阅[修改运行驱动程序堆栈](modifying-a-running-driver-stack.md)。

无法处理堆栈更改通知的协议驱动程序是适配器和重新绑定已解除。 不受影响的协议驱动程序已成功处理驱动程序堆栈通知绑定。

协议驱动程序应处理驱动程序堆栈暂停通知。 有关这些通知的详细信息，请参阅[暂停驱动程序堆栈](pausing-a-driver-stack.md)。

协议驱动程序应处理驱动程序堆栈重启通知。 有关这些通知的详细信息，请参阅[重新启动驱动程序堆栈](restarting-a-driver-stack.md)。

 

 





