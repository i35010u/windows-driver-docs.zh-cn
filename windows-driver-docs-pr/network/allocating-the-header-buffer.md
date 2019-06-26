---
title: 分配标头缓冲区
description: 分配标头缓冲区
ms.assetid: 7a6e87ce-a0b8-45ce-961e-f09d5ca919cb
keywords:
- 标头数据拆分 WDK，缓冲区分配
- 最大标头大小 WDK 标头数据拆分
- 缓冲区分配 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da6252aaf3691551266ac65aecf9e0765a0f9226
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384414"
---
# <a name="allocating-the-header-buffer"></a>分配标头缓冲区





NDIS 指定微型端口驱动程序应在分配的最大标头大小**MaxHeaderSize**的成员[ **NDIS\_HD\_拆分\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_hd_split_attributes)结构。 有关设置标头数据拆分属性的详细信息，请参阅[初始化标头数据拆分提供程序](initializing-a-header-data-split-provider.md)。

当一个 NIC 将拆分标头和接收的以太网帧中的数据时，所指示的以太网框架标头部分的大小不能超过**MaxHeaderSize**值。

如果 IP 标头包含 IPv4 选项、 IPsec 标头或 IPv6 扩展标头，并且标头超出了**MaxHeaderSize**值，NIC 必须不会拆分帧。

如果包括 UDP 标头、 TCP 标头或 TCP 选项的标头超过**MaxHeaderSize**值，NIC 必须拆分在帧[upper 层协议标头的开始](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)或不得拆分帧。

 

 





