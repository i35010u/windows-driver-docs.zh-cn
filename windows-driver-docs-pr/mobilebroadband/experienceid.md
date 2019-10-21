---
title: ExperienceID
description: ExperienceID
ms.assetid: 550527ae-fef9-46c6-816b-d842fe472b68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3effd9c4f887a7e8c44d8488d49ffdcf7097eb92
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323614"
---
# <a name="experienceid"></a>ExperienceID

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ExperienceID 元素指定表示设备体验的 GUID。 此 GUID 用于为与包的区域设置无关的相同设备标识符组合一个或多个元数据包。

在 Windows 8、Windows 8.1 和 Windows 10 中，它还用于将设备元数据链接到设备首次连接时可自动获取的设备应用。 设备应用在应用提交包的 Storemanifest.xml 文件中指定一个或多个 ExperienceID 元素。 其中每个 ExperienceID Guid 对应于设备元数据包的 ExperienceID 元素。 提交 Storemanifest.xml 文件后，如果设备应用 Storemanifest.xml 文件中还指定了设备的元数据中的 ExperienceID，则可将设备应用分发到一个或多个设备型号。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ExperienceID>
  text
</ExperienceID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


格式为[GUIDType](guidtype-packageinfo.md) XML 简单类型的值。

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
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">关系</a></p></td>
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">关系</a>元素指定用于在设备元数据缓存中跟踪设备元数据包的数据。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ExperienceID" type="tns:GUIDType" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


在 Windows 8.1 和 Windows 10 中，ExperienceID 是由 Windows 开发人员中心仪表板上的 "服务元数据" 向导创建的。

在 Windows 8 中，ExperienceID 可以由服务元数据开发人员指定，也可以使用[设备元数据创作向导](https://go.microsoft.com/fwlink/?linkid=620032)自动生成并添加到服务元数据中。 如果服务元数据包中未指定 ExperienceID，Windows 开发人员中心仪表板将创建一个 GUID，并在移动网络操作员或移动虚拟网络操作员提交服务元数据包。

 

 





