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
ms.openlocfilehash: 59ef846fe259895bc3a0c5ce0dff4a4ffe017fc3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357028"
---
# <a name="capturing-uncompressed-data-to-vram"></a>将未压缩的数据捕获到 VRAM


AVStream vram 能够启用了的微型驱动程序可以通过提供以下支持捕获 pin 描述符中的捕获未压缩的数据。

-   在相应[ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)结构，请列出捕获 pin 支持中的格式**DataRanges**成员、 数组[**KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)结构。 提供的指针到 KS\_DATARANGE\_视频结构，强制转换为指向 KSDATARANGE 的指针。

-   在中**VideoInfoHeader**的每个成员[ **KS\_DATARANGE\_视频**](https://msdn.microsoft.com/library/windows/hardware/ff567628)结构，请提供[ **KS\_VIDEOINFOHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff567700)结构。 每个 KS\_VIDEOINFOHEADER 包含[ **KS\_BITMAPINFOHEADER**](https://msdn.microsoft.com/library/windows/hardware/ff567305)。

-   若要公开了 MPEG2 捕获的二进制格式，设置**biCompression**等于 D3DDDIFMT\_BINARYBUFFER， **biHeight**等于一，和**biWidth**等于二进制缓冲区的大小。

*Capture.cpp*的文件[AVStream 模拟硬件示例驱动程序 (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)包含上述列表中的项的示例。

 

 




