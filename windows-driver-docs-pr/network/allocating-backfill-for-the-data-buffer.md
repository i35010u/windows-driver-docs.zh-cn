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
ms.openlocfilehash: ed03f808baab51a3dd6bb47581b6717a9b6b90f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367711"
---
# <a name="allocating-backfill-for-the-data-buffer"></a>为数据缓冲区分配回填





NDIS 指定微型端口驱动程序应分配中的数据回填空间量**BackfillSize**的成员[ **NDIS\_HD\_拆分\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565694)结构。 有关设置标头数据拆分属性的详细信息，请参阅[初始化标头数据拆分提供程序](initializing-a-header-data-split-provider.md)。

微型端口驱动程序时 NIC 将拆分标头和接收的以太网帧中的数据，必须将至少包含回填存储预分配的字节数的**BackfillSize**指定之前的数据部分的起始地址帧。 回填存储必须跨越页边界。

驱动程序堆栈可以使用预分配的回填存储复制的帧的标头部分并创建网络驱动程序无法处理的拆分以太网帧的几乎连续帧。

 

 





