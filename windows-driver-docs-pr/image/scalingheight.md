---
title: ScalingHeight 元素（慢速扫描方向）
description: 必需的 ScalingHeight 元素以慢速扫描方向指定文档缩放。
ms.assetid: 29dcaab0-d32b-4aa0-ba27-3da0c9c39f97
keywords:
- ScalingHeight 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScalingHeight wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: fb23d3bd7cfe7ce49aff28955f52233172f74df0
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020078"
---
# <a name="scalingheight-element-slow-scan-direction"></a>ScalingHeight 元素（慢速扫描方向）

必需的**ScalingHeight**元素以慢速扫描方向指定文档缩放。

## <a name="usage"></a>使用情况

```xml
<wscn:ScalingHeight wscn:Override="" wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ScalingHeight wscn:Override="" wscn:UsedDefault="">
```

## <a name="attributes"></a>属性

| 属性 | 类型 | 必须 | 说明 |
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
| [**扩展**](scaling.md) |

## <a name="remarks"></a>注解

**ScalingHeight**元素指定要应用在慢速扫描方向上的缩放比例。 缩放以1% 的增量表示，其中，值100表示100% 宽度刻度（不对文档高度进行调整）。

所有 WSD 扫描服务必须至少支持值100。

仅当**ScalingHeight**元素包含在**DocumentFinalParameters**层次结构中时，WSD 扫描服务才能指定可选**Override**和**UsedDefault**属性。 有关**Override**和**UsedDefault**及其用法的详细信息，请参阅[**DocumentFinalParameters**](documentfinalparameters.md)。

可以将此元素的允许值作为子集。

## <a name="see-also"></a>另请参阅

[**DocumentFinalParameters**](documentfinalparameters.md)

[**扩展**](scaling.md)

[**ScalingWidth**](scalingwidth.md)
