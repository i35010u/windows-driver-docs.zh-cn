---
title: 区域设置
description: 区域设置
ms.assetid: 1cf8d075-a1b3-4554-83d5-71fd5059c1c4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b42334d8726a9139214122d3b5d5fbed867171e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547961"
---
# <a name="locale"></a>区域设置

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

区域设置元素指定服务元数据包的区域设置。 服务元数据包可以指定单个或多个区域设置。 若要使用多个区域设置，必须设置[MultipleLocale](multiplelocale.md)元素**true**。

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
<th>属性</th>
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>默认</strong></p></td>
<td><p>xs:boolean</p></td>
<td><p>是</p></td>
<td><p>必须为 true (1) 或 false (0)。 如果默认属性设置为 true 时，此设备元数据打包为的默认值为当前区域设置的计算机的操作系统使用。</p></td>
</tr>
</tbody>
</table>

 

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


-   区域设置元素可以是 *&lt;语言&gt;* - *&lt;区域&gt;* （如 EN-US) 或 *&lt;语言&gt;* （例如 EN)。 如果 *&lt;语言&gt;* ，则包将应用于所有 *&lt;语言&gt;* 区域设置。 例如，EN 适用于 EN-US，EN-b.

-   若要指定的默认值为当前区域设置的计算机的元数据包，设置**默认**归于**true** (1)。

    **请注意**  应设置为服务只有一个元数据包**默认**归于**true** (1)。 否则，操作系统随机选择的服务元数据包。

     

-   时由操作系统选择要显示服务元数据包，它将使用的区域设置元素，如下所示：

    1.  操作系统中检索系统首选语言和区域。 这通常是在 Windows 安装过程中进行配置。

    2.  如果系统首选语言和区域，与匹配服务元数据包的区域设置元素，操作系统服务包中选择，并使用图标和**ServiceProvider** （从 ServiceInfo.xml) 的值，匹配该语言和区域。

    3.  如果服务元数据包没有与首选的系统语言相匹配的区域设置元素，操作系统将应用的语言中性图标和**ServiceProvider** （从 ServiceInfo.xml) 存储的值在服务元数据包的根。

区域设置元素是必需的。

 

 





