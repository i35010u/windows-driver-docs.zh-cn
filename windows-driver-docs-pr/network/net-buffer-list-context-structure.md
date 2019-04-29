---
title: NET_BUFFER_LIST_CONTEXT 结构
description: NET_BUFFER_LIST_CONTEXT 结构
ms.assetid: 45be8503-2c5f-46e6-9fc3-b1b3c42f0d91
keywords:
- NET_BUFFER_LIST_CONTEXT
- 网络数据 WDK，结构
- 数据 WDK 网络结构
- 数据包 WDK 网络、 数据结构
- 网络数据 WDK，上下文数据
- 数据 WDK 网络，上下文数据
- 数据包 WDK 网络的上下文数据
- 上下文 da
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc5666609e5751a93bc7aec1b5d30cafb5df4201
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380896"
---
# <a name="netbufferlistcontext-structure"></a>NET\_缓冲区\_列表\_上下文结构





使用 NDIS 驱动程序[ **NET\_缓冲区\_列表\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构，以存储与之关联的其他数据[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 **上下文**NET 成员\_缓冲区\_列表结构是指向 NET\_缓冲区\_列表\_上下文结构。 在 NET 中存储的信息\_缓冲区\_列表\_上下文结构是不透明的 NDIS 和堆栈中的其他驱动程序。

下图显示字段在 NET\_缓冲区\_列表\_上下文结构。

![说明在网络中的字段的关系图\-缓冲区\-列表\-上下文结构](images/netbufferlistcontext.png)

[ **NET\_缓冲区\_列表\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构包括**ContextData**包含上下文数据的成员。 此数据可以是驱动程序需要的任何上下文信息[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

驱动程序应使用以下 NDIS 宏和函数来访问和处理网络中的成员\_缓冲区\_列表\_上下文结构：

[**NdisAllocateNetBufferListContext**](https://msdn.microsoft.com/library/windows/hardware/ff561610)

[**NdisFreeNetBufferListContext**](https://msdn.microsoft.com/library/windows/hardware/ff562587)

[**NET\_缓冲区\_列表\_上下文\_数据\_开始**](https://msdn.microsoft.com/library/windows/hardware/ff568391)

[**NET\_BUFFER\_LIST\_CONTEXT\_DATA\_SIZE**](https://msdn.microsoft.com/library/windows/hardware/ff568390)

 

 





