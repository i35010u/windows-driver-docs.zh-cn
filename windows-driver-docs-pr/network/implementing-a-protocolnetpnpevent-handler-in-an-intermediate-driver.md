---
title: 实现一个中间驱动程序 ProtocolNetPnPEvent 处理程序
description: 在中间的驱动程序中实现 ProtocolNetPnPEvent 处理程序
ms.assetid: 1d0475c4-631d-4b8a-ab26-5b8b9425bfe6
keywords:
- ProtocolNetPnPEvent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dcaedd6a66f67e40ae9db6907d637dcc54a548a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519670"
---
# <a name="implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver"></a>在中间的驱动程序中实现 ProtocolNetPnPEvent 处理程序





实现[ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)中间驱动程序中的函数是协议驱动程序中实现几乎完全相同。 有关实现详细信息*ProtocolNetPnPEvent*处理程序中的中间驱动程序，请参阅[处理即插即用事件和协议驱动程序中的 PM 事件](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)。

NDIS 中间的驱动程序通过即插即用事件到更高的层驱动程序通过调用[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)函数。

 

 





