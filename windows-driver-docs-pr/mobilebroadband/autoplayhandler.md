---
title: AutoplayHandler
description: AutoplayHandler
ms.assetid: 0ee7ac9b-7c1a-4267-b718-ba110ef5b12d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53a0041d692a7208998922bef0bc32ffaabacfc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546289"
---
# <a name="autoplayhandler"></a>AutoplayHandler

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

AutoplayHandler 元素指定当用户插入设备时应显示为建议的自动播放操作的 UWP 设备应用程序。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<AutoplayHandler>
  child elements
</AutoplayHandler>
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
<td><p><a href="packageidentity.md" data-raw-source="[PackageIdentity](packageidentity.md)">PackageIdentity</a></p></td>
<td><p>为应用指定程序包标识 （名称和发布服务器）。</p></td>
</tr>
<tr class="even">
<td><p><a href="application-windowsinfo-v2.md" data-raw-source="[Application](application-windowsinfo-v2.md)">应用程序</a></p></td>
<td><p>指定应用程序的应用程序 ID。</p></td>
</tr>
<tr class="odd">
<td><p><a href="verb.md" data-raw-source="[Verb](verb.md)">Verb</a></p></td>
<td><p>指定该应用将注册的谓词。</p></td>
</tr>
<tr class="even">
<td><p><a href="autoplaytype.md" data-raw-source="[AutoplayType](autoplaytype.md)">AutoplayType</a></p></td>
<td><p>指定是否自动播放事件内容事件或的设备事件。 自动播放确定设备的类型，并引发卷设备的内容事件或非卷设备的设备事件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="enableautoplayforregisteredapps.md" data-raw-source="[EnableAutoPlayForRegisteredApps](enableautoplayforregisteredapps.md)">EnableAutoPlayForRegisteredApps</a></p></td>
<td><p>指定是否为已注册的应用程序启用自动播放。</p></td>
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
<td><p><a href="launchapplicationondeviceconnect.md" data-raw-source="[LaunchApplicationOnDeviceConnect](launchapplicationondeviceconnect.md)">LaunchApplicationOnDeviceConnect</a></p></td>
<td><p>指定当用户插入设备时应显示为建议的自动播放操作的应用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
      <xs:element name="AutoplayHandler" type="tns:AutoplayHandlerType" />

  <xs:complexType name="AutoplayHandlerType">
    <xs:sequence>
      <xs:element name="PackageIdentity" type="tns:PackageIdentityType" />
      <xs:element name="Application" type="tns:ApplicationType" />
      <xs:element name="Verb" type="tns:VerbType" />
      <xs:element name="AutoplayType" type="tns:AutoplayTypeType" />
      <xs:element name="EnableAutoPlayForRegisteredApps" type ="xs:boolean" default="false" minOccurs="0" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   结构[PackageIdentity](packageidentity.md)并[应用程序](application-windowsinfo-v2.md)元素与应用程序清单结构完全相同，因此应用程序的清单中的元素进行复制。

-   除了设备元数据中包含 AutoplayHandler 元素，指定的 UWP 设备应用还必须注册自动播放事件通过事件及其应用程序清单中添加一个声明。 自动播放识别应用程序的声明，并包括在用户可以用来响应该事件的可能操作的列表。

-   只有包中列出[DeviceCompanionApplications](devicecompanionapplications.md) SoftwareInfo.xml 文件中的值将作为设备安装的一部分下载。 如果[LaunchApplicationOnDeviceConnect](launchapplicationondeviceconnect.md)元素的值是从不同的包，Windows 不知道它将实际上是在用户设备上。 如果建议的应用程序不在用户的设备上，用户不可以看到与选择的选项。

-   即使应用程序是与相同[DeviceCompanionApplications](devicecompanionapplications.md)条目，它可能始终出现在自动播放列表。 如果用户未连接到 Internet 或无法下载的配套应用程序，则不会在列表中。 但是，当用户获取应用程序时，他们将看到"新选项可用"自动播放对话框的下次连接其设备。

AutoplayHandler 元素是可选的。

 

 





