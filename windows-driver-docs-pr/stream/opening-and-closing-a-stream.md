---
title: 打开和关闭流
description: 打开和关闭流
keywords:
- 视频捕获 WDK AVStream，打开流
- 捕获视频 WDK AVStream，打开流
- 视频捕获 WDK AVStream，关闭流
- 捕获视频 WDK AVStream，关闭流
- 打开流 WDK AVStream
- 关闭流 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f2e31b9636076f01893939f22fc43ea624377c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840519"
---
# <a name="opening-and-closing-a-stream"></a>打开和关闭流


Stream 类接口将 [**SRB \_ open \_ Stream**](./srb-open-stream.md) 请求发送到 stream 类微型驱动程序，以使用所选视频格式打开流。 传入的 SRB 打开流中的信息 \_ \_ 包括要打开的流的索引，以及指向 [**KS \_ VIDEOINFOHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader) 结构的指针的指针。 流索引对应于由微型驱动程序返回的 [**KS \_ DATARANGE \_ 视频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video) 结构数组中流的索引，以响应之前 [**SRB \_ 获取 \_ 流 \_ 信息**](./srb-get-stream-info.md) 请求。 有关处理 SRB \_ 获取流信息的详细信息 \_ \_ ，请参阅 [流类别](stream-categories.md)。

下面的示例代码获取流索引、内核流式处理数据格式和内核流视频信息标头。

```cpp
int StreamNumber = pSrb->StreamObject->StreamNumber;
PKS_DATAFORMAT_VIDEOINFOHEADER  pKSDataFormat = 
    (PKS_DATAFORMAT_VIDEOINFOHEADER) pSrb->CommandData.OpenFormat;
PKS_VIDEOINFOHEADER pVideoInfoHdrRequested = 
    &pKSDataFormat->VideoInfoHeader;
```

微型驱动程序应验证它们是否可支持请求的流格式。 特别是，应验证 [**KS \_ BITMAPINFOHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader) 结构的内容，以及 **rcSource** 和 **rcTarget** 成员指定的裁剪和缩放信息。

如果设备硬件无法支持 KS VIDEOINFOHEADER 的 **AvgTimePerFrame** 成员中请求的捕获帧速率 \_ ，则应始终选择下一个可用的 *lower* 帧速率。 例如，如果照相机可以支持每秒7帧的捕获帧速率 (fps) 15 fps，而客户端应用程序尝试以 10 fps 的捕获帧速率打开流，则照相机应创建 7 fps 物理流。

对于10秒的捕获，其中捕获了所有70个可用的物理帧，微型驱动程序应报告100帧，其中30帧已被 [**KSPROPERTY \_ DROPPEDFRAMES \_ CURRENT**](./ksproperty-droppedframes-current.md) 属性丢弃。

当输出缓冲区为 DirectDraw 图面时，将应用特殊规则。 在这种情况下，KS BITMAPINFOHEADER 结构的 **biWidth** 成员 \_ 实际上表示目标 DirectDraw 表面的跨距，这通常大于视频图像宽度。 图面的跨距通常是图面的宽度乘以其字节深度。 例如，对于宽度为640像素、颜色深度为每像素32位的图面，跨距为2560字节。

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

Stream 类接口将 [**SRB \_ close \_ 流**](./srb-close-stream.md) 请求发送到微型驱动程序以关闭流。 然后，微型驱动程序应将所有未完成的流 SRBs 返回到 Stream 类接口。

 

