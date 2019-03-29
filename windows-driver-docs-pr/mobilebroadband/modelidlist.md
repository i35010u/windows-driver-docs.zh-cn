---
title: ModelIDList
description: ModelIDList
ms.assetid: b7c6a100-95bf-421c-9a84-71623c0276fe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a560e4137f11615fed5a529ce0fcbf9f5dd50b5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566378"
---
# <a name="modelidlist"></a>ModelIDList

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ModelIDList 元素指定一个或多个 Guid。 通过指定每个 GUID [ModelID](modelid.md)元素，并标识设备元数据包中指定的物理设备。

**谨慎**   ModelIDList 和[ModelID](modelid.md)元素不支持的服务元数据包。 必须使用[HardwareIDList](hardwareidlist.md)并[HardwareID](hardwareid.md)元素相反。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ModelIDList>
  child elements
</ModelIDList>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


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
<td><p><a href="modelid.md" data-raw-source="[ModelID](modelid.md)">ModelID</a>元素指定的物理设备的 GUID。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a>元素指定设备元数据包的特性。 例如：</p>
<ul>
<li><p>每个设备支持的硬件函数的标识符。</p></li>
<li><p>特定于语言的区域设置的包中的文本字符串。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ModelIDList" type="tns:ModelIDListType" minOccurs="0" />

<xs:complexType name="ModelIDListType">
  <xs:sequence>
    <xs:element name="ModelID" type="tns:GUIDType" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


ModelIDList 元素是必需的仅当[HardwareIDList](hardwareidlist.md)元素中未指定[MetadataKey](metadatakey.md)元素。 如果指定，ModelIDList 元素必须包含一个或多个[ModelID](modelid.md)元素。 如果你的设备元数据包支持多个设备模型或模型 Id，则可以指定每个设备模型 ModelID 元素。

**谨慎**   ModelIDList 和[ModelID](modelid.md)元素不支持的服务元数据包。 必须使用[HardwareIDList](hardwareidlist.md)并[HardwareID](hardwareid.md)元素相反。

 

如果 PackageInfo XML 数据包含这两个[HardwareIDList](hardwareidlist.md)和 ModelIDList 元素，它确定设备是否由设备元数据包时操作系统使用的以下规则：

-   如果设备有一个模型 ID，操作系统不会搜索中的匹配项[HardwareIDList](hardwareidlist.md)元素。 模型 Id 的详细信息，请参阅[ModelID](modelid.md)。

-   否则，操作搜索[HardwareIDList](hardwareidlist.md)元素匹配的设备的硬件 id。

 

 





