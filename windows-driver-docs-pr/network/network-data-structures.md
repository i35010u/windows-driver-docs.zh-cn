---
title: 网络数据结构
description: 网络数据结构
ms.assetid: c29aaae6-6f68-404a-90dc-bae005ac9b6e
keywords:
- NET_BUFFER
- NET_BUFFER_LIST
- NET_BUFFER_LIST_CONTEXT
- 网络数据 WDK，结构
- 数据 WDK 网络结构
- 数据包 WDK 网络、 数据结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b78ea7cf518886afdba3899b584325a59b743553
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369889"
---
# <a name="network-data-structures"></a>网络数据结构





网络数据包含的发送或通过网络接收的数据包。 NDIS 提供的数据结构来描述和组织此类数据。 NDIS 6.0 及更高版本的主网络数据结构是：

-   [**NET\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff568376)
-   [**NET\_缓冲区列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)
-   [**NET\_BUFFER\_LIST\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff568389)

下图说明了这些结构之间的关系。

![演示如何 ndis 6.0 网络数据结构的关系图](images/netbufferstructures.png)

NDIS 6.0 及更高版本， [ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)是用于打包网络数据的基本构造块。 每个网络\_缓冲区结构具有 MDL 链。 MDLs 映射到数据缓冲区的数据的地址空间的 NET\_缓冲区结构指定。 此数据映射等同于 MDL 链接该 NDIS 5。*x*以及早期驱动程序中使用[ **NDIS\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff557086)结构。 NDIS 提供函数来操作 MDL 链。

多个 NET\_缓冲区结构可以附加到 NET\_缓冲区\_列表结构。 NET\_缓冲区结构组织为以 NULL 结尾的单向链接列表。 源自网络驱动程序\_缓冲区\_列表结构或 NDIS，应修改的链接的列表直接插入和删除 NET\_缓冲区结构。

[**NET\_缓冲区列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构包含用于描述所有信息[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)附加到列表的结构。 如果驱动程序的上下文信息需要额外的空间，该驱动程序可此类信息存储在 NET\_缓冲区\_列表\_上下文结构。 NDIS 提供可以分配、 释放和访问网络中的数据的函数\_缓冲区\_列表\_上下文结构。

多个 NET\_缓冲区\_列表结构可以附加到窗体中的 NET 列表\_缓冲区\_列表结构。 NET\_缓冲区\_列表结构组织为以 NULL 结尾的单向链接列表。 驱动程序可以修改的链接的列表直接插入和删除 NET\_缓冲区\_列表结构。

## <a name="related-topics"></a>相关主题


[**NET\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff568376)

[NET\_缓冲区结构](net-buffer-structure.md)

[**NET\_缓冲区列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

[NET\_缓冲区\_列表结构](net-buffer-list-structure.md)

[**NET\_BUFFER\_LIST\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff568389)

[NET\_缓冲区\_列表\_上下文结构](net-buffer-list-context-structure.md)

 

 






