---
title: ModelIDList
description: ModelIDList
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6463ef6e777251e4ce5e65e6147928462233a024
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805285"
---
# <a name="modelidlist"></a>ModelIDList

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

ModelIDList 元素指定一个或多个 Guid。 每个 GUID 都通过 [ModelID](modelid.md) 元素指定，并标识设备元数据包中指定的物理设备。

**警告**  
服务元数据包不支持 ModelIDList 和 [ModelID](modelid.md) 元素。 您必须改用 [HardwareIDList](hardwareidlist.md) 和 [HardwareID](hardwareid.md) 元素。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ModelIDList>
  child elements
</ModelIDList>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


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
<td><p><a href="modelid.md" data-raw-source="[ModelID](modelid.md)">ModelID</a></p></td>
<td><p><a href="modelid.md" data-raw-source="[ModelID](modelid.md)">ModelID</a>元素指定物理设备的 GUID。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a>元素指定设备元数据包的属性。 这些功能包括以下这些：</p>
<ul>
<li><p>设备支持的每个硬件功能的标识符。</p></li>
<li><p>包中的文本字符串的语言特定区域设置。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ModelIDList" type="tns:ModelIDListType" minOccurs="0" />

<xs:complexType name="ModelIDListType">
  <xs:sequence>
    <xs:element name="ModelID" type="tns:GUIDType" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


仅当[MetadataKey](metadatakey.md)元素中未指定[HardwareIDList](hardwareidlist.md)元素时，才需要 ModelIDList 元素。 如果已指定，则 ModelIDList 元素必须包含一个或多个 [ModelID](modelid.md) 元素。 如果设备元数据包支持多个设备模型或模型 Id，则可以为每个设备模型指定一个 ModelID 元素。

**警告**  
服务元数据包不支持 ModelIDList 和 [ModelID](modelid.md) 元素。 您必须改用 [HardwareIDList](hardwareidlist.md) 和 [HardwareID](hardwareid.md) 元素。

 

如果 PackageInfo XML 数据同时包含 [HardwareIDList](hardwareidlist.md) 和 ModelIDList 元素，则当操作系统确定设备元数据包是否指定了设备时，操作系统将使用以下规则：

-   如果设备具有模型 ID，操作系统将不会在 [HardwareIDList](hardwareidlist.md) 元素中搜索匹配项。 有关模型 Id 的详细信息，请参阅 [ModelID](modelid.md)。

-   否则，操作会在 [HardwareIDList](hardwareidlist.md) 元素中搜索设备的硬件 ID 的匹配项。

 

 





