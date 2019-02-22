---
title: DeviceNotificationHandler
description: DeviceNotificationHandler
ms.assetid: 04c4edb5-6dd1-4810-b23a-4f7ddc8af338
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b205e4e1cf09058c665ca8ea3a8c2446cabbc9df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545262"
---
# <a name="devicenotificationhandler"></a>DeviceNotificationHandler

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

DeviceNotificationHandler 元素指定设备通知处理程序。 设备通知处理程序，可运行代码以响应事件，如移动网络操作员管理短信或 USSD 通知，即使 Microsoft Store 应用未运行。 有关实现通知处理程序的详细信息，请参阅[移动运营商通知](https://go.microsoft.com/fwlink/?linkid=242062)白皮书。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<DeviceNotificationHandler EventID=”xs:string” EventAsset=”xs:string”/>
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
<td><p>EventID</p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p>设备通知处理程序事件 ID。</p></td>
</tr>
<tr class="even">
<td><p>EventAsset</p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p>设备通知处理程序事件资产。</p></td>
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
<td><p><a href="devicenotificationhandlers.md" data-raw-source="[DeviceNotificationHandlers](devicenotificationhandlers.md)">DeviceNotificationHandlers</a></p></td>
<td><p>指定设备通知处理程序。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="DeviceNotificationHandler" type="tns:DeviceNotificationHandlerType" maxOccurs="unbounded" />

<xs:complexType name="DeviceNotificationHandlerType">
  <xs:attribute name="EventID" type="xs:string" use="required"/>
  <xs:attribute name="EventAsset" type="xs:string" use="required"/>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   当您指定在 DeviceNotificationHandler[应用程序](application-softwareinfo-schema.md)元素中，系统调用事件处理程序，并调用时设备更改为状态的事件。

-   **EventID**属性是 SMS 设备用例 SMSEventHandler。

-   **EventAsset**属性是作为 Windows.BackgroundTasks 的扩展应用程序清单中指定的相同值。

DeviceNotificationHandler 元素是可选的。

 

 





