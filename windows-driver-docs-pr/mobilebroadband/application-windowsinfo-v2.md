---
title: '应用程序 (WindowsInfo) '
description: '应用程序 (WindowsInfo) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4a8ac808009072a4cf5bf62100aa8064b44a4f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782509"
---
# <a name="application-windowsinfo"></a>应用程序 (WindowsInfo) 

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

应用程序元素指定应用程序的应用程序 ID。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Application Id=”tns:ApplicationIdType” />
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
<th>必须</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ID</p></td>
<td><p>tns： ApplicationIdType</p></td>
<td><p>是</p></td>
<td><p>应用程序 ID。 从应用程序清单复制此值，如 "备注" 中所述。</p></td>
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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="autoplayhandler.md" data-raw-source="[AutoplayHandler](autoplayhandler.md)">AutoplayHandler</a></p></td>
<td><p>指定当用户插入设备时应显示为建议的自动播放操作的 UWP 设备应用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="Application" type="tns:ApplicationType" />

<xs:complexType name="ApplicationType">
  <xs:attribute name="Id" type="tns:ApplicationIdType" use="required"/>
</xs:complexType>

<xs:simpleType name="ApplicationIdType">
  <xs:restriction base="tns:AsciiWindowsIdType">
    <xs:maxLength value="64"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


应用程序元素的结构与应用 &lt; 程序清单中的应用程序元素的结构相对应 &gt; 。 从应用程序清单中的 Id 属性复制 Id 值的值。

下面的示例演示如何在 &lt; 应用程序 &gt; 清单中构造应用程序元素：

``` syntax
<Applications>
  <Application Id="DeviceAppForPrinters" Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForPrinters.App">
</Application>
</Applications>
```

应用程序元素是可选的。

 

 





