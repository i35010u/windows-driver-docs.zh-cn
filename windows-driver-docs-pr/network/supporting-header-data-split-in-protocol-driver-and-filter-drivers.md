---
title: 支持在协议和筛选器驱动程序中的标头数据拆分
description: 支持协议驱动程序和筛选器驱动程序中的标头数据拆分
ms.assetid: ba1566f2-7da6-4472-b00b-e25bf7acc294
keywords:
- 标头-数据拆分 WDK，协议驱动程序
- 标头-数据拆分 WDK，筛选器驱动程序
- 协议驱动程序 WDK 网络，标题-数据拆分
- 筛选器驱动程序 WDK 网络，标题-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fcfc782692858c430ccd9559511f2d511423e36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841799"
---
# <a name="supporting-header-data-split-in-protocol-drivers-and-filter-drivers"></a>支持协议驱动程序和筛选器驱动程序中的标头数据拆分





NDIS 6.0 和更高版本的协议驱动程序和筛选器驱动程序必须支持在非连续缓冲区中包含标头和数据的接收指示。

不得假设网络中只有一个 MDL [ **\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。 协议驱动程序和筛选器驱动程序不需要执行任何特定于支持标头数据拆分注册的操作。 但是，驱动程序接收处理代码必须处理 MDL 链中的一个或多个 MDL，并且必须使用以下 NDIS MDL 宏来访问 MDL 链：

-   [**NET\_BUFFER\_FIRST\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-first-mdl)

-   [**NET\_BUFFER\_当前\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-current-mdl)

-   [**NET\_BUFFER\_当前\_MDL\_偏移量**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-current-mdl-offset)

利用拆分缓冲区，与 NET\_缓冲区结构关联的数据长度（在[**网络\_缓冲区\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)结构中的**DataLength**成员中）会在多个 MDLs 之间拆分。 例如，如果某个协议驱动程序尝试访问第一个 MDL 中的整个数据缓冲区，则该驱动程序可以访问无效数据。

**请注意**  在接收指示调用返回到微型端口驱动程序后，微型端口驱动程序可以回收标头 MDLs。 在接收指示调用返回到微型端口驱动程序之后，过量驱动程序或其客户端不能访问标头 MDLs。 即使微型端口驱动程序未指明接收的数据的状态为 NDIS\_接收\_标志\_资源，此限制也适用。

 

 

 





