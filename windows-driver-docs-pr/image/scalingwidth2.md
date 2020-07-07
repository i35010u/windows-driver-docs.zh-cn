---
title: ScalingWidth 元素（输出文档）
description: 必需的 ScalingWidth 元素包含用于缩放输出文档宽度的允许值范围。
ms.assetid: 8b15f4b9-8537-479e-8745-0c8b35883bf5
keywords:
- ScalingWidth 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScalingWidth
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 29de9789434b4e3ee415ecf37eacc5795d1602ef
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020070"
---
# <a name="scalingwidth-element-output-document"></a>ScalingWidth 元素（输出文档）

必需的**ScalingWidth**元素包含用于缩放输出文档宽度的允许值范围。

## <a name="usage"></a>使用情况

```xml
<wscn:ScalingWidth>
  child elements
</wscn:ScalingWidth>
```

## <a name="attributes"></a>属性

没有特性。

## <a name="child-elements"></a>子元素

| 元素 |
|--|
| [**Timespan.maxvalue**](maxvalue.md) |
| [**MinValue**](minvalue.md) |

## <a name="parent-elements"></a>父元素

| 元素 |
|--|
| [**ScalingRangeSupported**](scalingrangesupported.md) |

## <a name="remarks"></a>注解

**ScalingWidth**元素包含[**MinValue**](minvalue.md)和[**元素，这些**](maxvalue.md)元素指定扫描设备支持的最小值和最大值，以便缩放输出文档的宽度。

**MinValue**和**MaxValue**必须是从**1 到 1000**的整数， **MinValue**小于或等于。 如果值为100，则表示扫描设备不应对扫描图像的宽度进行任何调整。 WSD 扫描服务至少必须支持100的值。

## <a name="see-also"></a>另请参阅

[**Timespan.maxvalue**](maxvalue.md)

[**MinValue**](minvalue.md)

[**ScalingHeight**](scalingheight2.md)

[**ScalingRangeSupported**](scalingrangesupported.md)
