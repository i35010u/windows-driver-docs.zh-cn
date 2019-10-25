---
title: 将未压缩的数据捕获到 VRAM
description: 将未压缩的数据捕获到 VRAM
ms.assetid: efec607d-3337-40a5-812c-57292f201d54
keywords:
- VRAM 捕获 WDK AVStream，未压缩的数据
- 未压缩的数据 WDK VRAM 捕获
- 格式化 WDK VRAM 捕获
- 固定 VRAM 处理 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bfad465f52cb814a8259c373ea7dc878463460d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844751"
---
# <a name="capturing-uncompressed-data-to-vram"></a>将未压缩的数据捕获到 VRAM


启用 VRAM 的 AVStream 微型驱动程序可以通过在捕获插针描述符中提供以下支持来捕获未压缩的数据。

-   在相应的[**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构中，列出了捕获 Pin 在**DataRanges**成员（ [**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构的数组）中支持的格式。 提供指向 KS\_DATARANGE 的指针\_视频结构，并将其强制转换为 KSDATARANGE 的指针。

-   在每个[**KS\_DATARANGE\_视频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)结构的**VideoInfoHeader**成员中，提供一个[**ks\_VideoInfoHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)结构。 每个 KS\_VIDEOINFOHEADER 都包含一个[**ks\_BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)。

-   若要为 MPEG2 捕获公开二进制格式，请将**biCompression**设置为等于 D3DDDIFMT\_BINARYBUFFER， **biHeight**等于 one， **biWidth**等于二进制缓冲区的大小。

[AVStream 模拟硬件示例驱动程序（AVSHwS）](https://go.microsoft.com/fwlink/p/?linkid=256083)的*捕获 .cpp*文件包含上列表中各项的示例。

 

 




