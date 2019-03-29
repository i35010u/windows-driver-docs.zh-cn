---
title: HardwareId (PackageInfo)
description: HardwareId (PackageInfo)
ms.assetid: edd05106-1bbc-45da-80cc-792d7fcce192
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb456db9e7a36c8aa891a3532d42588e2bc1b461
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575516"
---
# <a name="hardwareid-packageinfo"></a>HardwareId (PackageInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

有关服务元数据包的硬件 Id 值表示移动网络运营商采用以下形式：

-   GSM 网络：IMSI 值

-   GSM 网络：ICCID 值

-   CDMA 网络：提供程序名称值

-   CDMA 网络：提供程序 ID 值 (也称为 SID)

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<HardwareID>
  text
</HardwareID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


元数据创建过程中生成适当的硬件 ID 值涉及复杂的算法。 您应使用 MBIDGenerator.exe 包含 Windows Driver Kit (WDK) 中生成的硬件 ID 值。

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
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">HardwareIDList</a></p></td>
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">HardwareIDList</a>元素指定的服务元数据包的一个或多个硬件标识字符串。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="HardwareID" type="tns:HardwareIDType" maxOccurs="unbounded" />

<xs:simpleType name="HardwareIDType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="207" />
    <xs:pattern value="^([a-zA-Z0-9!#$%&()*+\-./:;&lt;=&gt;?@[\\\]^_`{|}~])*$" /> 
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   PackageInfo.xml 中包含的硬件 Id 都必须具有"DOID:"前缀添加到它们。 例如：DOID:MBAE:0:*hashednumber1*

-   多个硬件 Id 元素可用于指定的服务。

-   GSM IMSI 或 ICCID 范围的起始范围值必须以 00 结尾和结束范围值必须以 99 结尾。 出于隐私原因，匹配在 IMSI 和 ICCID 值 100 个的块。

HardwareID 元素是必需的。

 

 





