---
title: 选择 Stream 格式
description: 选择 Stream 格式
ms.assetid: 876eca52-4d5e-45bd-90df-ff4b6405078d
keywords:
- 视频捕获 WDK AVStream，流格式
- 捕获视频 WDK AVStream，流式传输格式
- 流格式 WDK 视频捕获
- 格式 WDK 视频捕获
- 执行数据交集 WDK 视频捕获
- 数据交集 WDK 视频捕获
- 交集 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5979f18fb5525c322a6681238f5be874da97d92d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556175"
---
# <a name="selecting-a-stream-format"></a>选择 Stream 格式


视频捕获设备可以捕获在许多不同的格式的视频。 [ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)结构用于传达有关宽度、 高度、 粒度，剪切、 信息和帧速率为特定颜色空间。 结构[ **KS\_DATARANGE\_视频**](https://msdn.microsoft.com/library/windows/hardware/ff567628)并[ **KS\_DATARANGE\_视频 2**](https://msdn.microsoft.com/library/windows/hardware/ff567629)是 KSDATARANGE 结构的扩展，应使用用于描述视频捕获格式。 使用 KS\_DATARANGE\_视频来描述仅视频帧。 使用 KS\_DATARANGE\_视频 2 来描述视频字段和视频帧，带或不带 bob 或将设置。

选择流格式的过程称为*执行数据交集*。 Stream 类接口发送[ **SRB\_获取\_数据\_交集**](https://msdn.microsoft.com/library/windows/hardware/ff568168)到 Stream 类微型驱动程序执行数据交集的请求。 微型驱动程序负责确定请求的数据范围的有效性，然后从提供的数据范围中，选择特定的流格式通常使用[ **KS\_DATAFORMAT\_VIDEOINFOHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff567331)或[ **KS\_DATAFORMAT\_VIDEOINFOHEADER2** ](https://msdn.microsoft.com/library/windows/hardware/ff567335)结构。

最后，微型驱动程序必须设置结果格式的特定成员，如下所示：

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

 

 




