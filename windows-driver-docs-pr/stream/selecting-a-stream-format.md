---
title: 选择流格式
description: 选择流格式
ms.assetid: 876eca52-4d5e-45bd-90df-ff4b6405078d
keywords:
- 视频捕获 WDK AVStream，流格式
- 捕获视频 WDK AVStream，流格式
- 流格式化 WDK 视频捕获
- 格式化 WDK 视频捕获
- 执行数据交集 WDK 视频捕获
- 数据交集 WDK 视频捕获
- 与 WDK 视频捕获交集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3aff211fc27a393debd5550032d66d3f3168f1dd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186315"
---
# <a name="selecting-a-stream-format"></a>选择流格式


视频捕获设备可以使用多种不同的格式捕获视频。 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85))结构用于传达有关特定颜色空间的宽度、高度、粒度、裁剪和帧速率的信息。 结构 [**KS \_ DATARANGE \_ VIDEO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video) 和 [**KS \_ DATARANGE \_ VIDEO2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video2) 是 KSDATARANGE 结构的扩展，应用于描述视频捕获格式。 使用 KS \_ DATARANGE \_ 视频仅描述视频帧。 使用 KS \_ DATARANGE \_ VIDEO2，可以使用或不使用 bob 或编织设置来描述视频字段和视频帧。

选择流格式的过程称为 *执行数据交集*。 Stream 类接口将 [**SRB \_ GET \_ 数据 \_ 交集**](./srb-get-data-intersection.md) 请求发送到 Stream 类微型驱动程序，以执行数据交集。 微型驱动程序负责确定请求的数据范围的有效性，然后从提供的数据范围中选择特定的流格式，通常使用 [**KS \_ DATAFORMAT \_ VIDEOINFOHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_videoinfoheader) 或 [**ks \_ DATAFORMAT \_ VIDEOINFOHEADER2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_videoinfoheader2) 结构。

最后，微型驱动程序必须设置生成的格式的某些成员，如下所示：

```cpp
.
.
.
// Calculate biSizeImage for this request, and put the result in both
// the biSizeImage field of the bmiHeader AND in the SampleSize field
// of the DataFormat.
//
// Note that for compressed sizes, this calculation will probably not
// be just width * height * bitdepth
 
DataFormatVideoInfoHeaderOut->VideoInfoHeader.bmiHeader.biSizeImage =
DataFormatVideoInfoHeaderOut->DataFormat.SampleSize = 
KS_DIBSIZE(DataFormatVideoInfoHeaderOut->VideoInfoHeader.bmiHeader);
.
.
```

 

