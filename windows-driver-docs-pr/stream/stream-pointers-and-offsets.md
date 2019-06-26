---
title: 流指针和偏移量
description: 流指针和偏移量
ms.assetid: ef9dc015-f0ee-49a6-8774-cfb0223c8b12
keywords:
- 流指针 WDK AVStream，偏移量
- WDK AVStream 的偏移量
- 流定位 WDK AVStream
- 输入定位 WDK AVStream
- 输出定位 WDK AVStream
- AVStream 指针 WDK
- AVStream 偏移量 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9831c5d658131c8e628d0110656fa6e479824fff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377795"
---
# <a name="stream-pointers-and-offsets"></a>流指针和偏移量





一个[ **KSSTREAM\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksstream_pointer)结构包含两个[ **KSSTREAM\_指针\_偏移量**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksstream_pointer_offset)索引在范围内的输入和输出位置的结构。 微型驱动程序可以处理这些偏移量或访问数据以帧分辨率。

若要继续学习在范围内的流指针，微型驱动程序调用[ **KsStreamPointerAdvanceOffsets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsets)并[ **KsStreamPointerAdvanceOffsetsAndUnlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock).

访问使用虚拟地址的流数据的微型驱动程序可以使用这些偏移量指定分辨率字节流的位置。 使用散播-聚集物理映射的微型驱动程序可以指定的流位置的粒度[ **KSMAPPING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksmapping)结构。

 

 




