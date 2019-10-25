---
title: 打开和关闭流
description: 打开和关闭流
ms.assetid: a4895e99-ab2e-482e-b89f-04b01177ec03
keywords:
- 视频捕获 WDK AVStream，打开流
- 捕获视频 WDK AVStream，打开流
- 视频捕获 WDK AVStream，关闭流
- 捕获视频 WDK AVStream，关闭流
- 打开流 WDK AVStream
- 关闭流 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a813eb3706ec01773261cea02d135a9bd5f9e260
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823514"
---
# <a name="opening-and-closing-a-stream"></a>打开和关闭流


Stream 类接口将[**SRB\_OPEN\_stream**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-stream)请求发送到 stream 类微型驱动程序，以使用所选视频格式打开流。 传递到 SRB\_打开\_流的信息包括要打开的流的索引，以及指向[**KS\_VIDEOINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)结构的指针的指针。 流索引对应于[**KS\_DATARANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)的数组中的流索引\_视频结构，由微型驱动程序返回，以响应之前的[**SRB\_获取\_流\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)请求。 有关处理 SRB\_获取\_STREAM\_信息的详细信息，请参阅[流类别](stream-categories.md)。

下面的示例代码获取流索引、内核流式处理数据格式和内核流视频信息标头。

```cpp
int StreamNumber = pSrb->StreamObject->StreamNumber;
PKS_DATAFORMAT_VIDEOINFOHEADER  pKSDataFormat = 
    (PKS_DATAFORMAT_VIDEOINFOHEADER) pSrb->CommandData.OpenFormat;
PKS_VIDEOINFOHEADER pVideoInfoHdrRequested = 
    &pKSDataFormat->VideoInfoHeader;
```

微型驱动程序应验证它们是否可支持请求的流格式。 特别是，应验证[**KS\_BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)结构的内容，以及**rcSource**和**rcTarget**成员指定的裁剪和缩放信息。

如果设备硬件无法支持 KS\_VIDEOINFOHEADER 的**AvgTimePerFrame**成员中请求的捕获帧速率，则应始终*选择下一个*可用的帧速率。 例如，如果照相机可以支持每秒7帧（fps）和 15 fps 的捕获帧速率，而客户端应用程序尝试以 10 fps 的捕获帧速率打开流，则照相机应创建 7 fps 物理流。

对于10秒的捕获，其中捕获了所有70个可用的物理帧，微型驱动程序应报告100帧，其中30帧已被[**KSPROPERTY\_DROPPEDFRAMES\_当前**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-droppedframes-current)属性丢弃。

当输出缓冲区为 DirectDraw 图面时，将应用特殊规则。 在这种情况下，KS\_BITMAPINFOHEADER 结构的**biWidth**成员实际上表示目标 DirectDraw 表面的跨距，通常大于视频图像宽度。 图面的跨距通常是图面的宽度乘以其字节深度。 例如，对于宽度为640像素、颜色深度为每像素32位的图面，跨距为2560字节。

若要确定请求的图像宽度，请使用以下代码示例：

```cpp
if (IsRectEmpty(&pVideoInfoHdrRequested->rcTarget) {
    Width =  pVideoInfoHdrRequested->bmiHeader.biWidth;
    Height = pVideoInfoHdrRequested->bmiHeader.biHeight;
} 
else {
    Width = pVideoInfoHdrRequested->rcTarget.right − 
            pVideoInfoHdrRequested->rcTarget.left;
    Height = pVideoInfoHdrRequested->rcTarget.bottom − 
             pVideoInfoHdrRequested->rcTarget.top;
}
```

Stream 类接口将[**SRB\_关闭\_流**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-close-stream)请求发送到微型驱动程序以关闭流。 然后，微型驱动程序应将所有未完成的流 SRBs 返回到 Stream 类接口。

 

 




