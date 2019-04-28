---
title: 指示已从微型端口驱动程序收到数据
description: 指示已从微型端口驱动程序收到数据
ms.assetid: da5d31e9-5212-4c6c-bac2-81432a46c303
keywords:
- 接收数据 WDK 网络
- NdisMIndicateReceiveNetBufferLists
- indicatings WDK NDIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 275fe244009dada90a2848ad8faee1ac5e680bc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327793"
---
# <a name="indicating-received-data-from-a-miniport-driver"></a>指示已从微型端口驱动程序收到数据





下图说明了微型端口驱动程序会收到指示。

![说明微型端口驱动程序的关系图会收到指示](images/miniportreceive.png)

微型端口驱动程序调用[ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)函数来指示接收来自网络的数据。 **NdisMIndicateReceiveNetBufferLists**函数将指示的列表传递[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构在堆栈中向上到基础驱动程序。

如果微型端口驱动程序设置**NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)，这表示微型端口驱动程序必须重新获得的所有权[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)立即结构。 在这种情况下，NDIS 不会调用微型端口驱动程序[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)函数以返回**NET\_缓冲区\_列表**结构。 微型端口驱动程序重新获得所有权后立即**NdisMIndicateReceiveNetBufferLists**返回。

如果未设置微型端口驱动程序不会**NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)，返回所指示的 NDIS [ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)到结构微型端口驱动程序[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)函数。 在这种情况下，微型端口驱动程序将放弃所指示的结构的所有权，直到 NDIS 返回到*MiniportReturnNetBufferLists*。

 

 





