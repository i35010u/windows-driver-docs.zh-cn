---
title: 流指针和偏移量
description: 流指针和偏移量
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
ms.openlocfilehash: dc6fed4aa7de4892674fa4ea11a5434cbbc3e2e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839843"
---
# <a name="stream-pointers-and-offsets"></a>流指针和偏移量





[**KSSTREAM \_ 指针**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer)结构包含两个 [**KSSTREAM \_ 指针 \_ 偏移**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer_offset)结构，它们对帧中的输入和输出位置进行索引。 微型驱动程序可以在帧解析时操作这些偏移量或访问数据。

若要在帧内前进流指针，微型驱动程序将调用 [**KsStreamPointerAdvanceOffsets**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets) 和 [**KsStreamPointerAdvanceOffsetsAndUnlock**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock)。

使用虚拟地址访问流数据的微型驱动程序可以使用这些偏移量在字节解析时指定流位置。 使用散点/集合物理映射的微型驱动程序可以按 [**KSMAPPING**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksmapping) 结构的粒度指定流位置。

 

