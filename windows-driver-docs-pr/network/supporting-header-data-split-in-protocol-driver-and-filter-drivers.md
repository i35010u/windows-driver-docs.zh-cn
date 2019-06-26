---
title: 支持标头数据拆分为协议和筛选器驱动程序
description: 支持协议驱动程序和筛选器驱动程序中的标头数据拆分
ms.assetid: ba1566f2-7da6-4472-b00b-e25bf7acc294
keywords:
- 标头数据拆分 WDK，协议驱动程序
- 标头数据拆分 WDK，筛选器驱动程序
- 协议驱动程序 WDK 网络，标头数据拆分
- 筛选器驱动程序 WDK 网络，标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef6b2ddf0327e6bc7f5bdad31e6ba5741aa77b54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381187"
---
# <a name="supporting-header-data-split-in-protocol-drivers-and-filter-drivers"></a>支持协议驱动程序和筛选器驱动程序中的标头数据拆分





NDIS 6.0 和更高版本的协议驱动程序和筛选器驱动程序必须支持不连续的缓冲区中接收与标头和数据的指示。

您必须假定是仅在单个 MDL [ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构。 协议驱动程序和筛选器驱动程序不需要执行任何操作特定于支持标头数据拆分注册。 但该驱动程序收到处理代码必须处理多个 MDL MDL 链中的，必须使用以下 NDIS MDL 宏来访问 MDL 链：

-   [**NET\_BUFFER\_FIRST\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-first-mdl)

-   [**NET\_BUFFER\_CURRENT\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-current-mdl)

-   [**NET\_BUFFER\_CURRENT\_MDL\_OFFSET**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-current-mdl-offset)

拆分缓冲的数据长度与该键相关联 NET\_缓冲区结构 (在**DataLength**的成员[ **NET\_缓冲区\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_data)结构) 跨多个 MDLs 拆分。 例如，如果尝试访问整个数据缓冲区中的第一个 MDL 协议驱动程序，该驱动程序无法访问无效数据。

**请注意**  微型端口驱动程序接收指示调用将返回到微型端口驱动程序后，可以回收 MDLs 的标头。 基础驱动程序或其客户端必须接收指示调用返回微型端口驱动程序之后访问的标头 MDLs。 此限制也适用甚至当微型端口驱动程序不指示接收到的数据与的 NDIS 状态\_接收\_标志\_资源。

 

 

 





