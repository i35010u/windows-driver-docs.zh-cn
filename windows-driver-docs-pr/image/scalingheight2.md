---
title: 'ScalingHeight 元素 (输出文档高度) '
description: 必需的 ScalingHeight 元素包含用于缩放输出文档高度的允许值范围。
keywords:
- ScalingHeight 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScalingHeight
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3d3797f5f9fcb5134831e103a7c6592f9e96b921
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822373"
---
# <a name="scalingheight-element-output-document-height"></a>ScalingHeight 元素 (输出文档高度) 

必需的 **ScalingHeight** 元素包含用于缩放输出文档高度的允许值范围。

## <a name="usage"></a>使用情况

```xml
<wscn:ScalingHeight>
  child elements
</wscn:ScalingHeight>
```

## <a name="attributes"></a>特性

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

## <a name="remarks"></a>备注

**ScalingHeight** 元素包含用于指定扫描设备支持的最小值和最大值的 [**MinValue**](minvalue.md) [**和个元素，用于**](maxvalue.md)缩放输出文档的高度。

**MinValue** 和 **MaxValue** 必须是从 **1 到 1000** 的整数， **MinValue** 小于或等于。 如果值为100，则表示扫描设备不应对扫描图像的高度进行任何调整。 WSD 扫描服务至少必须支持100的值。

## <a name="see-also"></a>请参阅

[**Timespan.maxvalue**](maxvalue.md)

[**MinValue**](minvalue.md)

[**ScalingRangeSupported**](scalingrangesupported.md)

[**ScalingWidth2**](scalingwidth.md)
