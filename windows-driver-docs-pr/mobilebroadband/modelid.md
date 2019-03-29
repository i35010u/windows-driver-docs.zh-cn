---
title: ModelID
description: ModelID
ms.assetid: 6873f5b6-453e-4f8e-b534-0bc805865905
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66dace2065e2d9ee6c87c6720e028c2dd89f5dec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564680"
---
# <a name="modelid"></a>ModelID

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ModelID 元素指定的物理设备的 GUID。

**谨慎**   [ModelIDList](modelidlist.md)和 ModelID 元素不支持的服务元数据包。 必须使用[HardwareIDList](hardwareidlist.md)并[HardwareID](hardwareid.md)元素相反。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ModelID>
  text
</ModelID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


一个值，格式为[GUIDType](guidtype-packageinfo.md) XML 的简单类型。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有子元素。

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a></p></td>
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a>元素指定每个支持的设备元数据包中指定的设备的硬件模型的 GUID。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


ModelID 元素指定支持的设备的硬件模型的模型 ID。 通过 GUID 指定每个模型 ID。

**谨慎**   [ModelIDList](modelidlist.md)和 ModelID 元素不支持的服务元数据包。 必须使用[HardwareIDList](hardwareidlist.md)并[HardwareID](hardwareid.md)元素相反。

 

模型 Id 基于业务定义或 SKU 的物理设备。 每个模型 ID 必须是唯一的所有品牌和型号的物理设备。

以下列表描述了硬件和模型 Id。 对于物理设备之间的差异：

-   通过指定硬件 Id [HardwareID](hardwareid.md)元素，标识硬件函数基于特定于总线的值。 硬件 Id 可以将设备驱动程序映射到设备实例。 例如，具有相同的硬件 ID 的两个设备共享相同的驱动程序使用的功能接口。

-   通过 ModelID 元素指定的模型 Id 启用来唯一标识物理设备的总线或接口技术独立的 OEM 或独立硬件供应商 (IHV)。 例如，具有不同的模型 Id 的两个设备可能具有其组件的相同硬件 Id。

-   硬件 Id 将映射到特定的总线或接口上的设备实例的设备元数据包。

-   模型 Id 映射到物理设备，而不考虑如何将设备连接到计算机的设备元数据包。

 

 





