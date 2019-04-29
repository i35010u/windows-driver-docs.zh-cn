---
title: 指定流格式
description: 指定流格式
ms.assetid: 60ef129c-f4a1-4eb5-97d9-6be6c7803258
keywords:
- 视频捕获 WDK AVStream，流格式
- 捕获视频 WDK AVStream，流式传输格式
- 流格式 WDK 视频捕获
- 格式 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9438d9c0151e83b5f9bdd035c5184af76a3e9eb1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360822"
---
# <a name="specifying-stream-formats"></a>指定流格式


通常情况下，DirectShow 和内核共享媒体流式处理格式定义和流式处理的转换。 在内核模式和用户模式组件使用的命名约定中的差异有些模糊不清此一致性。 许多媒体格式和内核模式中使用的 GUID 定义具有前缀*KS\_* 但除此之外，与对应的用户模式相同。 例如，Win32 用户模式版本的内核模式结构[ **KS\_BITMAPINFOHEADER**](https://msdn.microsoft.com/library/windows/hardware/ff567305)，是 BITMAPINFOHEADER。

视频捕获微型驱动程序描述了特定的流格式使用[ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)结构。 但是，微型驱动程序还可以公开了大量的潜在 stream 的格式通过指定的数组[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)结构。 KSDATARANGE 结构描述图像特征，例如颜色格式、 位深度和裁剪和缩放的可能性。

单个 KSDATARANGE 结构可以描述数千个潜在 KSDATAFORMAT 结构。 例如，KSDATARANGE 结构可以用最小尺寸为 160 x 120 像素和 720 x 480 像素，最大维度粒度单步执行大小中值为 1 x 和 y 维度指定 RGB24 示例的视频流。 此操作，请从应用程序可以请求任何唯一 KSDATAFORMAT 结构时，通过超过 200,000 个可能的输出图像尺寸。

DirectShow 使用类似于 KSDATAFORMAT 的结构来定义流格式。 例如：

```cpp
typedef struct  _AMMediaType    {
    GUID majortype;            // Same as KSDATAFORMAT.MajorFormat
    GUID subtype;              // Same as KSDATAFORMAT.SubFormat
    BOOL bFixedSizeSamples;
    BOOL bTemporalCompression;
    ULONG lSampleSize;         // Same as KSDATAFORMAT.SampleSize
    GUID formattype;           // Same as KSDATAFORMAT.Specifier
    IUnknown __RPC_FAR *pUnk;
    ULONG cbFormat;
    BYTE *pbFormat;
 } AM_MEDIA_TYPE;
```

尽管在命名约定，在内核模式 KSDATARANGE/KSDATAFORMAT 和用户模式中使用的 Guid 的区别是\_媒体\_类型结构是否相同。

**请注意**  :低序位四个字节**子格式**KSDATAFORMAT 结构中的成员 (这就是类似于**子类型**AM 成员\_媒体\_类型用户模式结构)应匹配中使用的 FOURCC 值**biCompression**的成员[ **KS\_BITMAPINFOHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff567305)结构。 这两个字节包含描述一种格式，按相反的顺序的十六进制 ASCII 字符。

例如，以下 GUID 对应于 YVU9 FOURCC 视频格式：

```Text
39555659-0000-0010-8000-00AA00389B71
      59 = 'Y'
    56 = 'V'
  55 = 'U'
39 = '9'
```
