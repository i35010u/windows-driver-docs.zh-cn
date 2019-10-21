---
title: HardwareId (PackageInfo)
description: HardwareId (PackageInfo)
ms.assetid: edd05106-1bbc-45da-80cc-792d7fcce192
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb456db9e7a36c8aa891a3532d42588e2bc1b461
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323700"
---
# <a name="hardwareid-packageinfo"></a>HardwareId (PackageInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

对于服务元数据包，HardwareID 值表示移动网络操作员，格式如下：

-   GSM 网络： IMSI 值

-   GSM 网络： ICCID 值

-   CDMA 网络：提供程序名称值

-   CDMA 网络：提供程序 ID 值（也称为 SID）

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<HardwareID>
  text
</HardwareID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


在元数据创建过程中生成正确的硬件 ID 值涉及复杂的算法。 应该使用 Windows 驱动程序工具包（WDK）中包含的 MBIDGenerator 生成硬件 ID 值。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有子元素。

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
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">HardwareIDList</a></p></td>
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">HardwareIDList</a>元素指定服务元数据包的一个或多个硬件标识字符串。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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


-   PackageInfo 中包含的硬件 Id 必须向其添加 "DOID：" 前缀。 例如： DOID： MBAE：0：*hashednumber1*

-   多个 HardwareID 元素可用于指定一个服务。

-   对于 GSM IMSI 或 ICCID 范围，开始范围值必须以00结束，结束范围值必须以99结束。 出于隐私原因，IMSI 和 ICCID 值的100块中发生匹配。

HardwareID 元素是必需的。

 

 





