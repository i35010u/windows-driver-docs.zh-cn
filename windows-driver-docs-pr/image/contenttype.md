---
title: ContentType 元素
description: 可选 ContentType 元素指定原始文档的主要特征。
keywords:
- ContentType 元素图像处理设备
topic_type:
- apiref
api_name:
- wscn ContentType wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: e8af6e46619f42b1e6ddb2c8bc5dc3f9a7618475
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826883"
---
# <a name="contenttype-element"></a>ContentType 元素

可选 **ContentType** 元素指定原始文档的主要特征。

## <a name="usage"></a>使用情况

```xml
<wscn:ContentType wscn:MustHonor="" wscn:Override="" wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ContentType wscn:MustHonor="" wscn:Override="" wscn:UsedDefault="">
```

## <a name="attributes"></a>特性

| 属性 | 类型 | 必须 | 描述 |
|--|--|--|--|
| MustHonor | xs:string | 否 | 可选。 必须为0、false、1或 true 的布尔值。 |
| 替代 | xs:string | 否 | 可选。 必须为0、false、1或 true 的布尔值。 |
| UsedDefault | xs:string | 否 | 可选。 必须为0、false、1或 true 的布尔值。 |

## <a name="text-value"></a>文本值

必需。 以下值之一：

|术语  |描述  |
|---------|---------|
|自动     |      扫描设备将自动检测原始类型。   |
|文本     |     他的文档主要由不同的文本组成，这与背景对比强烈。    |
|照片     |     原始的主要由照片图像组成，其中的阴影变化逐渐增加，边缘并不明显。    |
|色     |   原始的主要包括 halftoned 映像。      |
|Mixed     |     具有多个特定 DocumentType 特征的多页文档。    |

可以扩展此元素的值并为其赋值。

## <a name="child-elements"></a>子元素

没有任何子元素。

## <a name="parent-elements"></a>父元素

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

## <a name="remarks"></a>备注

仅当 **ContentType** 元素包含在 **CreateScanJobRequest** 层次结构内时，客户端才能指定可选的 **MustHonor** 属性。 有关 **MustHonor** 及其用法的详细信息，请参阅 [**CreateScanJobRequest**](createscanjobrequest.md)。

仅当 **ContentType** 元素包含在 **DocumentFinalParameters** 层次结构中时，WSD 扫描服务才能指定可选 **Override** 和 **UsedDefault** 属性。 有关 **Override** 和 **UsedDefault** 及其用法的详细信息，请参阅 [**DocumentFinalParameters**](documentfinalparameters.md)。

## <a name="see-also"></a>请参阅

[**CreateScanJobRequest**](createscanjobrequest.md)
