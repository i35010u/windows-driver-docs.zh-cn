---
title: ConnectionInfo
description: ConnectionInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1af7880bbc08debe3962f0c737b2c9947afbe67
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782473"
---
# <a name="connectioninfo"></a>ConnectionInfo


ConnectionInfo 元素为指定的运算符指定连接列表。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ConnectionInfoList AccessString=”xs:string” Username=”xs:string” Password=”xs:string” FriendlyName=”xs:string” Purchase=”xs:Boolean” Internet=”xs:Boolean” AutoConnectOrder=”xs:positiveinteger” Compression=”xs:token” AutoProtocol=”xs:token”>
</ConnectionInfoList>
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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AccessString</p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p>操作员的名称和国家/地区。</p>
<p>示例： Contoso (阿根廷) </p></td>
</tr>
<tr class="even">
<td><p>用户名</p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p>用户名用于连接到 Internet。</p></td>
</tr>
<tr class="odd">
<td><p>密码</p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p>用于连接到 Internet 的密码。</p></td>
</tr>
<tr class="even">
<td><p>FriendlyName</p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p>"接入点" 下拉框中的 "Windows 连接管理器" 中显示的值。</p></td>
</tr>
<tr class="odd">
<td><p>购买</p></td>
<td><p>xs:boolean</p></td>
<td><p>是</p></td>
<td><p>指示是否应将访问字符串用于购买或 Internet。</p></td>
</tr>
<tr class="even">
<td><p>Internet</p></td>
<td><p>xs:boolean</p></td>
<td><p>是</p></td>
<td><p>指示是否应将访问字符串用于购买或 Internet。</p></td>
</tr>
<tr class="odd">
<td><p>AutoConnectOrder</p></td>
<td><p>xs： positiveinteger</p></td>
<td><p>否</p></td>
<td><p>确定 Windows 尝试连接到 <a href="connectioninfolist.md" data-raw-source="[ConnectionInfoList](connectioninfolist.md)">ConnectionInfoList</a> 元素中的每个 APNs 的顺序。</p></td>
</tr>
<tr class="even">
<td><p>压缩</p></td>
<td><p>xs:token</p></td>
<td><p>否</p></td>
<td><p>指定是否在数据链路上使用压缩来标头和数据传输。</p>
<p>值：启用或禁用</p></td>
</tr>
<tr class="odd">
<td><p>AuthProtocol</p></td>
<td><p>xs:token</p></td>
<td><p>否</p></td>
<td><p>指定用于激活 PDP 上下文的身份验证协议。</p>
<p>值： NONE、PAP、CHAP 或 Eap-mschapv2</p></td>
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
<td><p><a href="connectioninfolist.md" data-raw-source="[ConnectionInfoList](connectioninfolist.md)">ConnectionInfoList</a></p></td>
<td><p>指定 APN 数据库中操作员的详细信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element ref="ConnectionInfo" maxOccurs="unbounded"/>

<xs:element name="ConnectionInfo">
  <xs:complexType>
    <xs:attribute name="AccessString" use="optional">
      <!--The AccessString element identifies the APN or dial string to be used to establish a data connection -->
      <xs:simpleType>
        <xs:restriction base="xs:string">
          <xs:minLength value="0"/>
          <xs:maxLength value="100"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
    <xs:attribute name="Username" use="optional">
      <!--The UserName element specifies the user name for logon -->
      <xs:simpleType>
        <xs:restriction base="xs:string">
          <xs:minLength value="0"/>
          <xs:maxLength value="255"/>
          <xs:whiteSpace value="collapse"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
    <xs:attribute name="Password" use="optional">
      <xs:simpleType>
        <xs:restriction base="xs:string">
          <xs:minLength value="0"/>
          <xs:maxLength value="255"/>
          <xs:whiteSpace value="collapse"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
    <xs:attribute name="FriendlyName" use="optional">
      <xs:simpleType>
        <xs:restriction base="xs:string">
          <xs:minLength value="0"/>
          <xs:maxLength value="255"/>
          <xs:whiteSpace value="collapse"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
    <xs:attribute name="Purchase" type="xs:boolean" use="required"/>
    <xs:attribute name="Internet" type="xs:boolean" use="required"/>
    <xs:attribute name="AutoConnectOrder" type="xs:positiveInteger" use="optional"/>
    <xs:attribute name="Compression" use="optional">
      <xs:simpleType>
        <xs:restriction base="xs:token">
          <xs:enumeration value="DISABLE"/>
          <xs:enumeration value="ENABLE"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
    <xs:attribute name="AuthProtocol" use="optional">
      <xs:simpleType>
        <xs:restriction base="xs:token">
          <xs:enumeration value="NONE"/>
          <xs:enumeration value="PAP"/>
          <xs:enumeration value="CHAP"/>
          <xs:enumeration value="MsCHAPv2"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
  </xs:complexType>
</xs:element>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


ConnectionInfo 元素是必需的。

 

 





