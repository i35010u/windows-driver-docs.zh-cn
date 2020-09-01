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
ms.openlocfilehash: a1e3d2f206a4fe61b44a69bda460ec05868f802a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188777"
---
# <a name="capturing-uncompressed-data-to-vram"></a>将未压缩的数据捕获到 VRAM

启用 VRAM 的 AVStream 微型驱动程序可以通过在捕获插针描述符中提供以下支持来捕获未压缩的数据。

- 在相应的 [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor) 结构中，列出了捕获 pin 在 **DataRanges** 成员（ [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构的数组）中支持的格式。 提供指向 KS \_ DATARANGE \_ 视频结构的指针，该结构强制转换为指向 KSDATARANGE 的指针。

- 在每个[**ks \_ DATARANGE \_ 视频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)结构的**VideoInfoHeader**成员中，提供一个[**ks \_ VideoInfoHeader**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)结构。 每个 KS \_ VIDEOINFOHEADER 都包含一个 [**ks \_ BITMAPINFOHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)。

- 若要为 MPEG2 捕获公开二进制格式，请将 **biCompression** 设置为等于 D3DDDIFMT \_ BINARYBUFFER，将 **biHeight** 等于 one，并将 **biWidth** 设置为等于二进制缓冲区的大小。

[AVStream 模拟硬件示例驱动程序 (AVSHwS) ](/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)的*捕获 .cpp*文件包含上列表中各项的示例。