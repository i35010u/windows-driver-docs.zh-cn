---
title: 将未压缩的数据捕获到 VRAM
description: 将未压缩的数据捕获到 VRAM
ms.assetid: efec607d-3337-40a5-812c-57292f201d54
keywords:
- VRAM 捕获 WDK AVStream，未压缩的数据
- 未压缩的数据 WDK VRAM 捕获
- 格式化 WDK VRAM 捕获
- 固定 VRAM 处理 WDK AVStream
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 128cd3c4d05a1d8da1ca0205b8674dd17b7bd152
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812451"
---
# <a name="capturing-uncompressed-data-to-vram"></a>将未压缩的数据捕获到 VRAM

启用 VRAM 的 AVStream 微型驱动程序可以通过在捕获插针描述符中提供以下支持来捕获未压缩的数据。

- 在相应的[**KSPIN \_ 描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构中，列出了捕获 pin 在**DataRanges**成员（ [**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构的数组）中支持的格式。 提供指向 KS \_ DATARANGE \_ 视频结构的指针，该结构强制转换为指向 KSDATARANGE 的指针。

- 在每个[**ks \_ DATARANGE \_ 视频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)结构的**VideoInfoHeader**成员中，提供一个[**ks \_ VideoInfoHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)结构。 每个 KS \_ VIDEOINFOHEADER 都包含一个[**ks \_ BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)。

- 若要为 MPEG2 捕获公开二进制格式，请将**biCompression**设置为等于 D3DDDIFMT \_ BINARYBUFFER，将**biHeight**等于 one，并将**biWidth**设置为等于二进制缓冲区的大小。

[AVStream 模拟硬件示例驱动程序（AVSHwS）](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)的*捕获 .cpp*文件包含上列表中各项的示例。
