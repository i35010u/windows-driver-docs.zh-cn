---
title: ModelID
description: ModelID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a400550534e9fe07ae1c22ef70288ee7cc1ac40
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823057"
---
# <a name="modelid"></a>ModelID

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

ModelID 元素指定物理设备的 GUID。

**警告**  
服务元数据包不支持 [ModelIDList](modelidlist.md) 和 ModelID 元素。 您必须改用 [HardwareIDList](hardwareidlist.md) 和 [HardwareID](hardwareid.md) 元素。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ModelID>
  text
</ModelID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


格式为 [GUIDType](guidtype-packageinfo.md) XML 简单类型的值。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有任何子元素。

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


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
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a>元素指定设备元数据包中指定的设备所支持的每个硬件型号的 GUID。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


ModelID 元素指定设备支持的硬件型号的模型 ID。 每个模型 ID 都通过 GUID 来指定。

**警告**  
服务元数据包不支持 [ModelIDList](modelidlist.md) 和 ModelID 元素。 您必须改用 [HardwareIDList](hardwareidlist.md) 和 [HardwareID](hardwareid.md) 元素。

 

模型 Id 基于物理设备的业务定义或 SKU。 每个模型 ID 对于物理设备的所有构成和型号都必须是唯一的。

以下列表描述了物理设备的硬件和型号 Id 之间的差异：

-   硬件 Id，通过 [HardwareID](hardwareid.md) 元素指定，基于特定于总线的值识别硬件功能。 硬件 Id 可能会将设备驱动程序映射到设备实例。 例如，两个具有相同硬件 ID 的设备共享同一驱动程序使用的功能接口。

-   模型 Id 通过 ModelID 元素指定，使 OEM 或独立硬件供应商 (IHV) 可以唯一地标识独立于总线或接口技术的物理设备。 例如，两个具有不同模型 Id 的设备可能为其组件具有相同的硬件 Id。

-   硬件 Id 将设备元数据包映射到特定总线或接口上的设备实例。

-   无论设备连接到计算机的方式如何，模型 Id 都将设备元数据包映射到物理设备。

 

 





