---
title: 为数据缓冲区分配回填
description: 为数据缓冲区分配回填
ms.assetid: 2588986d-8d51-4f34-a3b9-d0df406afcba
keywords:
- 标头-数据拆分 WDK，回填分配
- 回填空间分配 WDK 标头-数据拆分
- 预分配的回填存储 WDK 标头-数据拆分
- 数据回填空间 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 524ff4899573d2b2c9d73136b2961fa384546eeb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835316"
---
# <a name="allocating-backfill-for-the-data-buffer"></a>为数据缓冲区分配回填





NDIS 指定微型端口驱动程序应在[**NDIS\_HD\_SPLIT\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)结构的**BackfillSize**成员中分配的数据回填空间量。 有关设置标头数据拆分属性的详细信息，请参阅[初始化标头-数据拆分提供程序](initializing-a-header-data-split-provider.md)。

当 NIC 在收到的以太网帧中拆分标头和数据时，微型端口驱动程序必须将至少**BackfillSize**指定的字节数预分配到帧的数据部分的起始地址之前。 回填存储不得跨页面边界。

驱动程序堆栈可以使用预分配的回填存储来复制该帧的标头部分，并为无法处理拆分的以太网帧的网络驱动程序创建一个近乎连续的帧。

 

 





