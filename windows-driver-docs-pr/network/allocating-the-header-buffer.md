---
title: 分配标头缓冲区
description: 分配标头缓冲区
ms.assetid: 7a6e87ce-a0b8-45ce-961e-f09d5ca919cb
keywords:
- 标头-数据拆分 WDK，缓冲区分配
- 最大标头大小 WDK 标头-数据拆分
- 缓冲区分配 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2d9a25c77f490659062b7a0d5d5f2eda7cf74fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835290"
---
# <a name="allocating-the-header-buffer"></a>分配标头缓冲区





NDIS 指定微型端口驱动程序应在[**NDIS\_HD\_SPLIT\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)结构的**MaxHeaderSize**成员中分配的最大标头大小。 有关设置标头数据拆分属性的详细信息，请参阅[初始化标头-数据拆分提供程序](initializing-a-header-data-split-provider.md)。

当 NIC 在收到的以太网帧中拆分标头和数据时，所指示的以太网帧的标头部分的大小不得超过**MaxHeaderSize**值。

如果 IP 标头包含 IPv4 选项、IPsec 标头或 IPv6 扩展标头，并且如果标头超过**MaxHeaderSize**值，则 NIC 不得拆分此帧。

如果包含 UDP 标头、TCP 标头或 TCP 选项的标头超出了**MaxHeaderSize**值，则 NIC 必须将帧拆分为[上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)，或者不得拆分此帧。

 

 





