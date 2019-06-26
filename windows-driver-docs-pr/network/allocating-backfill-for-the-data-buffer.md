---
title: 为数据缓冲区分配回填
description: 为数据缓冲区分配回填
ms.assetid: 2588986d-8d51-4f34-a3b9-d0df406afcba
keywords:
- 标头数据拆分 WDK，回填分配
- 回填空间分配 WDK 标头数据拆分
- 预分配的回填存储 WDK 标头数据拆分
- 数据回填空间 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 226ce041f1509f86f82514932429447adcdcbede
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386359"
---
# <a name="allocating-backfill-for-the-data-buffer"></a>为数据缓冲区分配回填





NDIS 指定微型端口驱动程序应分配中的数据回填空间量**BackfillSize**的成员[ **NDIS\_HD\_拆分\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_hd_split_attributes)结构。 有关设置标头数据拆分属性的详细信息，请参阅[初始化标头数据拆分提供程序](initializing-a-header-data-split-provider.md)。

微型端口驱动程序时 NIC 将拆分标头和接收的以太网帧中的数据，必须将至少包含回填存储预分配的字节数的**BackfillSize**指定之前的数据部分的起始地址帧。 回填存储必须跨越页边界。

驱动程序堆栈可以使用预分配的回填存储复制的帧的标头部分并创建网络驱动程序无法处理的拆分以太网帧的几乎连续帧。

 

 





