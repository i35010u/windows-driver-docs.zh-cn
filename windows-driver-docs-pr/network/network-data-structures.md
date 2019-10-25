---
title: 网络数据结构
description: 网络数据结构
ms.assetid: c29aaae6-6f68-404a-90dc-bae005ac9b6e
keywords:
- NET_BUFFER
- NET_BUFFER_LIST
- NET_BUFFER_LIST_CONTEXT
- 网络数据 WDK，结构
- 数据 WDK 网络，结构
- 包 WDK 网络，数据结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28de665bbeacbfd2e568eb758847197b7c1f69fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827243"
---
# <a name="network-data-structures"></a>网络数据结构





网络数据包含通过网络发送或接收的数据包。 NDIS 提供了用于描述和组织此类数据的数据结构。 用于 NDIS 6.0 和更高版本的主网络数据结构为：

-   [**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)
-   [**NET\_缓冲区列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)
-   [**NET\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)

下图说明了这些结构之间的关系。

![说明 ndis 6.0 网络数据结构的示意图](images/netbufferstructures.png)

在 NDIS 6.0 和更高版本中， [**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)是用于封装网络数据的基本构建基块。 每个网络\_缓冲器结构都有一个 MDL 链。 MDLs 将数据缓冲区的地址映射到 NET\_BUFFER 结构指定的数据空间。 此数据映射与 NDIS 5 的 MDL 链完全相同。*x*及更早版本的驱动程序在[**NDIS\_数据包**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构中使用。 NDIS 提供操作 MDL 链的函数。

可以将多个 NET\_缓冲器结构附加到网络\_缓冲器\_列表结构。 NET\_缓冲区结构被组织为以 NULL 结尾的单向链接列表。 只有产生了 NET\_BUFFER\_列表结构或 NDIS 的驱动程序才应该直接修改链接列表，以插入和删除 NET\_缓冲区结构。

[**NET\_BUFFER list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构包含描述附加到列表的所有[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的信息。 如果驱动程序需要额外的空间来存储上下文信息，则驱动程序可以将此类信息存储在网络\_缓冲区\_列表\_的上下文结构。 NDIS 提供函数以分配、释放和访问 NET\_缓冲区\_列表\_上下文结构中的数据。

可以附加多个 NET\_缓冲区\_列表结构，以形成一系列网络\_缓冲区\_列表结构。 NET\_缓冲区\_列表结构组织为以 NULL 结尾的单向链接列表。 驱动程序可以直接修改链接列表，以插入和删除 NET\_BUFFER\_列表结构。

## <a name="related-topics"></a>相关主题


[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)

[NET\_缓冲区结构](net-buffer-structure.md)

[**NET\_缓冲区列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[NET\_BUFFER\_列表结构](net-buffer-list-structure.md)

[**NET\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)

[NET\_缓冲区\_列表\_上下文结构](net-buffer-list-context-structure.md)

 

 






