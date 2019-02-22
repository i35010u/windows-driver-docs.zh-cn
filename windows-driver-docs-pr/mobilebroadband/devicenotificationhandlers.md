---
title: DeviceNotificationHandlers
description: DeviceNotificationHandlers
ms.assetid: 94661e6a-97ed-4dbf-ab09-b39545ee2e40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6e20cb59754fdb97a725a5ccaa9e42e01ff174a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546905"
---
# <a name="devicenotificationhandlers"></a>DeviceNotificationHandlers

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

DeviceNotificationHandlers 元素指定设备通知处理程序。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<DeviceNotificationHandlers>
  Child element
</DeviceNotificationHandlers>
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
<td><p><a href="devicenotificationhandler.md" data-raw-source="[DeviceNotificationHandler](devicenotificationhandler.md)">DeviceNotificationHandler</a></p></td>
<td><p>指定设备通知处理程序。</p></td>
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
<td><p><a href="application-softwareinfo-schema.md" data-raw-source="[Application](application-softwareinfo-schema.md)">应用程序</a></p></td>
<td><p>指定在 PC 上检测到操作员的移动宽带硬件时将下载的应用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="DeviceNotificationHandlers" type="tns:DeviceNotificationHandlersType" minOccurs="0" />

<xs:complexType name="DeviceNotificationHandlersType">
  <xs:sequence>
    <xs:element name="DeviceNotificationHandler" type="tns:DeviceNotificationHandlerType" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


DeviceNotificationHandlers 元素是可选的。

 

 





