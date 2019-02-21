---
title: ExperienceID
description: ExperienceID
ms.assetid: 550527ae-fef9-46c6-816b-d842fe472b68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3effd9c4f887a7e8c44d8488d49ffdcf7097eb92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524306"
---
# <a name="experienceid"></a>ExperienceID

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ExperienceID 元素指定一个 GUID，表示设备体验。 此 GUID 用于组相同的设备标识符独立于包的区域设置的一个或多个元数据包。

在 Windows 8、 Windows 8.1 和 Windows 10 它还用于链接到首次连接设备时可以自动获取的设备应用程序的设备元数据。 设备应用在应用程序提交包中的 StoreManifest.XML 文件中指定一个或多个 ExperienceID 元素。 每个这些 ExperienceID Guid 对应于设备元数据包的 ExperienceID 元素。 提交 StoreManifest.xml 文件后，设备应用程序然后，可以分发到一个或多个设备模型，如果设备应用 StoreManifest 文件中还指定设备的元数据中 ExperienceID。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ExperienceID>
  text
</ExperienceID>
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
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">关系</a></p></td>
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">关系</a>元素指定用于跟踪设备元数据包设备元数据缓存中的数据。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ExperienceID" type="tns:GUIDType" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


在 Windows 8.1 和 Windows 10 中，ExperienceID 创建由 Windows 开发人员中心仪表板上的服务元数据向导。

在 Windows 8 中 ExperienceID 可以指定服务元数据开发人员，或自动生成并添加到服务的元数据使用[设备元数据创建向导](https://go.microsoft.com/fwlink/?linkid=620032)。 如果 ExperienceID 未指定服务元数据包中，Windows 开发人员中心仪表板创建的 GUID 和时移动网络运营商或移动虚拟网络运营商将提交更新的元数据的包中的 ExperienceID 元素服务元数据包。

 

 





