---
title: ColorEntry 元素
description: 必需的 ColorEntry 元素描述扫描仪上的输入源支持的单个颜色处理模式。
keywords:
- ColorEntry 元素图像设备
topic_type:
- apiref
api_name:
- wscn ColorEntry
api_type:
- Schema
ms.date: 11/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1d36eee7dcb7282a4aa3dffb6eddc021b28e39c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823187"
---
# <a name="colorentry-element"></a>ColorEntry 元素

必需的 **ColorEntry** 元素描述扫描仪上的输入源支持的单个颜色处理模式。

## <a name="usage"></a>使用情况

```xml
<wscn:ColorEntry>
  text
</wscn:ColorEntry>
```

## <a name="attributes"></a>特性

没有特性。

## <a name="text-value"></a>文本值

必需。 以下关键字之一：

| 术语 | 描述 |
|--|--|
| BlackAndWhite1 | 黑色和白色图像;1位/像素 (bpp) 和单个通道 |
| Grayscale4 | 灰度图像;4 bpp 和单通道 |
| Grayscale8 | 灰度图像;8 bpp 和单通道 |
| Grayscale16 | 灰度图像;16 bpp 和单通道 |
| RGB24 | RGB 编码的颜色图像;24 bpp 分别分为8位的三个通道 |
| RGB48 | RGB 编码的颜色图像;48 bpp 分别分为三个16位通道 |
| RGBa32 | 带有 alpha 通道的 RGB 编码颜色图像;32位 bpp 分为每个8位通道 |
| RGBa64 | 带有 alpha 通道的 RGB 编码颜色图像;64 bpp 分别分为16位的四个通道 |

## <a name="child-elements"></a>子元素

没有任何子元素。

## <a name="parent-elements"></a>父元素

[**ADFColor**](adfcolor.md)

[**FilmColor**](filmcolor.md)

[**PlatenColor**](platencolor.md)

## <a name="remarks"></a>备注

每个 value 关键字描述颜色数据类型和编码、位深度和每个通道的位数。 下表显示了值关键字如何映射到扫描仪的颜色处理属性。

| 关键字 | 像素位深度 | 每通道位数 |
|--|--|--|
| BlackAndWhite1 | 1 | 1 |
| Grayscale4 | 4 | {4} |
| Grayscale8 | 8 | {8} |
| Grayscale16 | 16 | {16} |
| RGB24 | 24 | {8,8,8} |
| RGB48 | 48 | {16,16,16} |
| RGBa32 | 32 | {8,8,8,8} |
| RGBa64 | 64 | {16,16,16,16} |

可以扩展和子集化此元素的允许值。
