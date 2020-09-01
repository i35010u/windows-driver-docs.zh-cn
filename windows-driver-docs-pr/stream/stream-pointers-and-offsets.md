---
title: 流指针和偏移量
description: 流指针和偏移量
ms.assetid: ef9dc015-f0ee-49a6-8774-cfb0223c8b12
keywords:
- 流指针 WDK AVStream，偏移量
- 偏移 WDK AVStream
- 流位置 WDK AVStream
- 输入位置 WDK AVStream
- 输出位置 WDK AVStream
- AVStream 指针 WDK
- AVStream 偏移 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09d98c7e4a70ddb092c087997af3945d52d64b29
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186261"
---
# <a name="stream-pointers-and-offsets"></a>流指针和偏移量





[**KSSTREAM \_ 指针**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer)结构包含两个[**KSSTREAM \_ 指针 \_ 偏移**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer_offset)结构，它们对帧中的输入和输出位置进行索引。 微型驱动程序可以在帧解析时操作这些偏移量或访问数据。

若要在帧内前进流指针，微型驱动程序将调用 [**KsStreamPointerAdvanceOffsets**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets) 和 [**KsStreamPointerAdvanceOffsetsAndUnlock**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock)。

使用虚拟地址访问流数据的微型驱动程序可以使用这些偏移量在字节解析时指定流位置。 使用散点/集合物理映射的微型驱动程序可以按 [**KSMAPPING**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksmapping) 结构的粒度指定流位置。

 

