---
title: 为数据缓冲区分配回填
description: 为数据缓冲区分配回填
keywords:
- 标头-数据拆分 WDK，回填分配
- 回填空间分配 WDK 标头-数据拆分
- 预分配的回填存储 WDK 标头-数据拆分
- 数据回填空间 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19726114da1bf23f6660d60b900370e2c724f124
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820125"
---
# <a name="allocating-backfill-for-the-data-buffer"></a>为数据缓冲区分配回填





NDIS 指定微型端口驱动程序应在 [**NDIS \_ HD \_ SPLIT \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)结构的 **BackfillSize** 成员中分配的数据回填空间量。 有关设置标头数据拆分属性的详细信息，请参阅 [初始化 Header-Data 拆分提供程序](initializing-a-header-data-split-provider.md)。

当 NIC 在收到的以太网帧中拆分标头和数据时，微型端口驱动程序必须将至少 **BackfillSize** 指定的字节数预分配到帧的数据部分的起始地址之前。 回填存储不得跨页面边界。

驱动程序堆栈可以使用预分配的回填存储来复制该帧的标头部分，并为无法处理拆分的以太网帧的网络驱动程序创建一个近乎连续的帧。

 

