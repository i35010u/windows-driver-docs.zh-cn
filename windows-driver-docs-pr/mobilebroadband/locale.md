---
title: Locale
description: Locale
ms.assetid: 1cf8d075-a1b3-4554-83d5-71fd5059c1c4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e244c37a274d0679b10731ee3224d063cc75c84
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403354"
---
# <a name="locale"></a>Locale

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

Locale 元素指定服务元数据包的区域设置。 服务元数据包可以指定单个或多个区域设置。 若要使用多个区域设置，则必须将 [MultipleLocale](multiplelocale.md) 元素设置为 **true**。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Locale
  default = "xs:boolean">
  text
</Locale>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>类型</th>
<th>必选</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>default</strong></p></td>
<td><p>xs:boolean</p></td>
<td><p>是</p></td>
<td><p> (1) 或 false (0) 必须为 true。 如果将默认属性设置为 "true"，则操作系统将此设备元数据包用作计算机当前区域设置的默认值。</p></td>
</tr>
</tbody>
</table>

 

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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a>元素指定设备元数据包的属性。 其中包括：</p>
<ul>
<li><p>设备支持的每个硬件功能的标识符。</p></li>
<li><p>包中的文本字符串的语言特定区域设置。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="Locale" type="tns:LocaleType" />

<xs:complexType name="LocaleType">
  <xs:simpleContent>
    <xs:extension base="xs:string">
      <xs:attribute name="default" type="xs:boolean" use="required" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   区域设置元素可以是* &lt; 语言 &gt; * - * &lt; 区域 &gt; * (例如 en-us) 或* &lt; language &gt; * (，如 en) 。 如果设置了* &lt; 语言 &gt; * ，则包适用于所有* &lt; 语言 &gt; *区域设置。 例如，EN 适用于 EN-US 和 ZH-CN。

-   若要将元数据包指定为计算机当前区域设置的默认值，请将 **默认** 属性设置为 **true** (1) 。

    **注意**   对于一个服务，只应将**默认**属性设置为**true** (1) 。 否则，操作系统会随机选择服务的元数据包。

     

-   当操作系统选择要显示的服务元数据包时，它将按以下方式使用 Locale 元素：

    1.  操作系统检索系统首选语言和区域。 通常在 Windows 安装程序过程中配置此设置。

    2.  如果服务元数据包的 Locale 元素与系统首选语言和区域相匹配，则操作系统将为服务选择包，并使用与该语言和区域匹配的 ServiceInfo.xml) 中 (的图标和 **ServiceProvider** 值。

    3.  如果服务元数据包没有与系统首选语言相匹配的 Locale 元素，则操作系统将应用从服务元数据包的根目录中存储的 ServiceInfo.xml)  (的语言中性图标和 **ServiceProvider** 值。

Locale 元素是必需的。

 

 





