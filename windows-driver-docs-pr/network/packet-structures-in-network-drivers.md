---
title: 网络驱动程序中的数据包结构
description: 网络驱动程序中的数据包结构
ms.assetid: 01989a73-3f68-431a-ab77-b61f03265c22
keywords:
- 数据包 WDK 网络
- 网络驱动程序 WDK，数据包
- 网络数据 WDK
- 数据 WDK 网络
- 网络数据包结构 WDK
- 网络数据缓冲区 WDK
- 数据缓冲区 WDK 网络
- 网络数据 WDK，结构
- 数据 WDK 网络结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce6457858795a35bce59d022c0c3262bbb24e45e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566790"
---
# <a name="packet-structures-in-network-drivers"></a>网络驱动程序中的数据包结构





在 NDIS 6.0 和更高版本中，更高的层驱动程序分配[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)并[ **NET\_缓冲区列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构来保存网络数据包的信息，并将结构发送到下一个较低的 NDIS 驱动程序，以便可以在网络上发送数据。 较低级别的驱动程序分配 NET\_缓冲区和 NET\_缓冲区\_列表结构来保留接收的数据和最多传递结构关注更高层的驱动程序。 有时，更高的层驱动程序分配结构，并将其传递到较低层驱动程序具有较低层驱动程序将接收到的数据复制到提供的缓冲区的请求。 NDIS 提供了用于分配和操作组成 NET 子结构的函数\_缓冲区和 NET\_缓冲区\_列表结构。

有关网络 NDIS 驱动程序中的数据缓冲区的结构的详细信息，请参阅[NET\_缓冲体系结构](net-buffer-architecture.md)。

 

 





