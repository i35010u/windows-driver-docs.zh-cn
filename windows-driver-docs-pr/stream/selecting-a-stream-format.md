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
ms.openlocfilehash: d464f3604888513a92bbc3d45c865cd74475f36c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843321"
---
# <a name="selecting-a-stream-format"></a>选择流格式


视频捕获设备可以使用多种不同的格式捕获视频。 [**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构用于传达有关特定颜色空间的宽度、高度、粒度、裁剪和帧速率的信息。 结构[**KS\_DATARANGE\_视频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)和[**KS\_DATARANGE\_VIDEO2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video2)是 KSDATARANGE 结构的扩展，应用于描述视频捕获格式。 使用 KS\_DATARANGE\_视频来仅描述视频帧。 使用 KS\_DATARANGE\_VIDEO2，可以使用或不使用 bob 或编织设置来描述视频字段和视频帧。

选择流格式的过程称为*执行数据交集*。 Stream 类接口发送 SRB\_获取对 Stream 类微型驱动程序的[ **\_数据\_交集**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-data-intersection)请求，以执行数据交集。 微型驱动程序负责确定请求的数据范围的有效性，然后从提供的数据范围中选择特定的流格式，通常使用[**KS\_DATAFORMAT\_VIDEOINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_videoinfoheader)或[**KS\_DATAFORMAT\_VIDEOINFOHEADER2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_videoinfoheader2)结构。

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

 

 




