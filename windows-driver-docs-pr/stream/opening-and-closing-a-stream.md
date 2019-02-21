---
title: 打开和关闭 Stream
description: 打开和关闭 Stream
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
ms.openlocfilehash: d9004de0fb5108653c7e532679c5bde7954cb3da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533327"
---
# <a name="opening-and-closing-a-stream"></a>打开和关闭 Stream


Stream 类接口发送[ **SRB\_打开\_流**](https://msdn.microsoft.com/library/windows/hardware/ff568191)到 Stream 类微型驱动程序的请求，以使用所选的视频格式打开一个流。 信息传入 SRB\_打开\_流包含要在打开的流和指向指针的索引[ **KS\_VIDEOINFOHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff567700)结构。 流索引对应的数组中的流的索引[ **KS\_DATARANGE\_视频**](https://msdn.microsoft.com/library/windows/hardware/ff567628)返回的响应早期微型驱动程序的结构[**SRB\_获取\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff568173)请求。 有关详细信息，了解如何处理 SRB\_获取\_流\_信息，请参阅[Stream 类别](stream-categories.md)。

下面的代码示例获取流索引、 内核流式处理数据格式和流式处理视频信息标头的内核。

```cpp
int StreamNumber = pSrb->StreamObject->StreamNumber;
PKS_DATAFORMAT_VIDEOINFOHEADER  pKSDataFormat = 
    (PKS_DATAFORMAT_VIDEOINFOHEADER) pSrb->CommandData.OpenFormat;
PKS_VIDEOINFOHEADER pVideoInfoHdrRequested = 
    &pKSDataFormat->VideoInfoHeader;
```

微型驱动程序应验证可以支持请求的流格式。 具体而言的内容[ **KS\_BITMAPINFOHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff567305)应验证结构裁剪和缩放指定的信息以及**时**并**rcTarget**成员。

如果设备硬件无法支持请求中所捕获的帧速率**AvgTimePerFrame** KS 成员\_VIDEOINFOHEADER，它应始终选择下一步*低*帧速率可用。 例如，如果照相机可以支持的第二个 (fps) 和 15 fps，每 7 帧捕获帧速率和客户端应用程序尝试打开流中的 10 个 fps 捕获帧速率，照相机应创建 7 fps 物理流。

对于在其中捕获所有 70 的可用物理帧的十秒捕获，微型驱动程序应报告 100 帧捕获，30 帧的已删除通过[ **KSPROPERTY\_DROPPEDFRAMES\_当前**](https://msdn.microsoft.com/library/windows/hardware/ff565135)属性。

当输出缓冲区已 DirectDraw 图面，将应用特殊规则。 在这种情况下， **biWidth** KS 成员\_BITMAPINFOHEADER 结构实际上表示目标 DirectDraw 表面通常大于视频图像宽度的步幅。 一个面步幅通常是乘以其字节深度图面的宽度。 例如，640 像素宽颜色深度的 32 位每像素的图面，对于跨距将为 2560 个字节。

若要确定请求的图像宽度，请使用下面的代码示例：

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

Stream 类接口发送[ **SRB\_关闭\_流**](https://msdn.microsoft.com/library/windows/hardware/ff568165)关闭流到微型驱动程序请求。 然后，微型驱动程序应返回所有未完成的流 Srb，到 Stream 类接口。

 

 




