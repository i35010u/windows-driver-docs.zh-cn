---
title: AutoplayHandler
description: AutoplayHandler
ms.assetid: 0ee7ac9b-7c1a-4267-b718-ba110ef5b12d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cace5cb820535a93ed575479e54f72ba12812966
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402890"
---
# <a name="autoplayhandler"></a>AutoplayHandler

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

AutoplayHandler 元素指定在用户插入设备时应显示为建议的自动播放操作的 UWP 设备应用。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<AutoplayHandler>
  child elements
</AutoplayHandler>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


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
<td><p><a href="packageidentity.md" data-raw-source="[PackageIdentity](packageidentity.md)">PackageIdentity</a></p></td>
<td><p>指定应用的包标识 (名称和发布服务器) 。</p></td>
</tr>
<tr class="even">
<td><p><a href="application-windowsinfo-v2.md" data-raw-source="[Application](application-windowsinfo-v2.md)">应用程序</a></p></td>
<td><p>指定应用程序的应用程序 ID。</p></td>
</tr>
<tr class="odd">
<td><p><a href="verb.md" data-raw-source="[Verb](verb.md)">谓词</a></p></td>
<td><p>指定应用注册的谓词。</p></td>
</tr>
<tr class="even">
<td><p><a href="autoplaytype.md" data-raw-source="[AutoplayType](autoplaytype.md)">AutoplayType</a></p></td>
<td><p>指定自动播放事件是否为设备事件或内容事件。 自动播放会确定设备类型，并为非卷设备引发设备事件，或为卷设备引发内容事件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="enableautoplayforregisteredapps.md" data-raw-source="[EnableAutoPlayForRegisteredApps](enableautoplayforregisteredapps.md)">EnableAutoPlayForRegisteredApps</a></p></td>
<td><p>指定是否为已注册的应用启用自动播放。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="launchapplicationondeviceconnect.md" data-raw-source="[LaunchApplicationOnDeviceConnect](launchapplicationondeviceconnect.md)">LaunchApplicationOnDeviceConnect</a></p></td>
<td><p>指定当用户插入设备时应显示为建议的自动播放操作的应用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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


-   [PackageIdentity](packageidentity.md)和[应用](application-windowsinfo-v2.md)程序元素的结构与应用程序清单结构相同，因此请复制应用程序清单中的元素。

-   除了在设备元数据中包含 AutoplayHandler 元素外，指定的 UWP 设备应用还必须通过在事件的应用程序清单中添加声明来注册自动播放事件。 自动播放识别应用程序的声明，然后将其包含在用户可以执行以响应该事件的可能操作列表中。

-   只会在安装设备的过程中下载 SoftwareInfo.xml 文件中的 [DeviceCompanionApplications](devicecompanionapplications.md) 值中列出的程序包。 如果 [LaunchApplicationOnDeviceConnect](launchapplicationondeviceconnect.md) 元素的值来自于不同的包，则 Windows 不知道它是否将实际位于用户的设备上。 如果建议的应用程序不在用户的设备上，则将不会向用户显示所选的。

-   即使应用程序与 [DeviceCompanionApplications](devicecompanionapplications.md) 项相同，它也不会始终出现在 "自动播放" 列表中。 如果用户未连接到 Internet 或无法下载伴生应用程序，则它将不会出现在列表中。 但是，当用户获取应用程序时，将在下次连接其设备时，显示 "新选项可用" 的 "自动播放" 对话框。

AutoplayHandler 元素是可选的。

 

 





