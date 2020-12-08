---
title: 'ScalingWidth 元素 (快速扫描方向) '
description: 必需的 ScalingWidth 元素按快速扫描方向指定文档缩放。
keywords:
- ScalingWidth 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScalingWidth wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8ca5d9604e97d703686033518952004f99773e3f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822367"
---
# <a name="scalingwidth-element-fast-scan-direction"></a>ScalingWidth 元素 (快速扫描方向) 

必需的 **ScalingWidth** 元素按快速扫描方向指定文档缩放。

## <a name="usage"></a>使用情况

```xml
<wscn:ScalingWidth wscn:Override="" wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ScalingWidth wscn:Override="" wscn:UsedDefault="">
```

## <a name="attributes"></a>特性

| 属性 | 类型 | 必须 | 描述 |
|--|--|--|--|
| **忽略** | xs:string | 否 | 可选。 必须为0、false、1或 true 的布尔值。 |
| **UsedDefault** | xs:string | 否 | 可选。 必须为0、false、1或 true 的布尔值。 |

## <a name="text-value"></a>文本值

必需。 介于1到1000（含）范围内的整数。

## <a name="child-elements"></a>子元素

没有任何子元素。

## <a name="parent-elements"></a>父元素

| 元素 |
|--|
| [**缩放**](scaling.md) |

## <a name="remarks"></a>备注

**ScalingWidth** 元素指定要在快速扫描方向上应用的缩放比例。 缩放以1% 的增量表示，其中值为100表示100% 宽度刻度 (没有调整文档宽度) 。

所有 WSD 扫描服务必须至少支持值100。

仅当 **ScalingWidth** 元素包含在 **DocumentFinalParameters** 层次结构中时，WSD 扫描服务才能指定可选 **Override** 和 **UsedDefault** 属性。 有关 **Override** 和 **UsedDefault** 及其用法的详细信息，请参阅 [**DocumentFinalParameters**](documentfinalparameters.md)。

可以将此元素的允许值作为子集。

## <a name="see-also"></a>请参阅

[**DocumentFinalParameters**](documentfinalparameters.md)

[**缩放**](scaling.md)

[**ScalingHeight**](scalingheight.md)
