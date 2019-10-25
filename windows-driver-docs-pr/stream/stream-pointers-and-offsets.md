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
ms.openlocfilehash: c76a994350d09af95a2a3f2183cc93a2640c4b16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837676"
---
# <a name="stream-pointers-and-offsets"></a>流指针和偏移量





[**KSSTREAM\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer)结构包含两个[**KSSTREAM\_指针\_偏移**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer_offset)结构，它们对帧中的输入和输出位置进行索引。 微型驱动程序可以在帧解析时操作这些偏移量或访问数据。

若要在帧内前进流指针，微型驱动程序将调用[**KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets)和[**KsStreamPointerAdvanceOffsetsAndUnlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock)。

使用虚拟地址访问流数据的微型驱动程序可以使用这些偏移量在字节解析时指定流位置。 使用散点/集合物理映射的微型驱动程序可以按[**KSMAPPING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksmapping)结构的粒度指定流位置。

 

 




