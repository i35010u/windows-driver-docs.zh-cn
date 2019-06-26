---
title: 将未压缩的数据捕获到 VRAM
description: 将未压缩的数据捕获到 VRAM
ms.assetid: efec607d-3337-40a5-812c-57292f201d54
keywords:
- Vram 能够捕获 WDK AVStream，未压缩数据
- WDK vram 能够捕获的未压缩的数据
- 格式 WDK vram 能够捕获
- pin vram 能够处理 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2591c90b824ef820933c212b71c88761b4a86c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386664"
---
# <a name="capturing-uncompressed-data-to-vram"></a>将未压缩的数据捕获到 VRAM


AVStream vram 能够启用了的微型驱动程序可以通过提供以下支持捕获 pin 描述符中的捕获未压缩的数据。

-   在相应[ **KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)结构，请列出捕获 pin 支持中的格式**DataRanges**成员、 数组[**KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构。 提供的指针到 KS\_DATARANGE\_视频结构，强制转换为指向 KSDATARANGE 的指针。

-   在中**VideoInfoHeader**的每个成员[ **KS\_DATARANGE\_视频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_video)结构，请提供[ **KS\_VIDEOINFOHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_videoinfoheader)结构。 每个 KS\_VIDEOINFOHEADER 包含[ **KS\_BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)。

-   若要公开了 MPEG2 捕获的二进制格式，设置**biCompression**等于 D3DDDIFMT\_BINARYBUFFER， **biHeight**等于一，和**biWidth**等于二进制缓冲区的大小。

*Capture.cpp*的文件[AVStream 模拟硬件示例驱动程序 (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)包含上述列表中的项的示例。

 

 




