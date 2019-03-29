---
title: ConnectionInfo
description: ConnectionInfo
ms.assetid: bbdba286-4d28-46b6-bafa-83cbddd883ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 464350735044c190486fe9b18d9b944d59fb957d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565359"
---
# <a name="connectioninfo"></a>ConnectionInfo


ConnectionInfo 元素指定对于指定的运算符连接的列表。

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
<th>特性</th>
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AccessString</p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p>名称和国家/地区的运算符。</p>
<p>例如：Contoso （阿根廷）</p></td>
</tr>
<tr class="even">
<td><p>Username</p></td>
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
<td><p>显示 Windows 连接管理器中的 APN 下拉列表框中的值。</p></td>
</tr>
<tr class="odd">
<td><p>购买</p></td>
<td><p>xs:boolean</p></td>
<td><p>是</p></td>
<td><p>表示是否应为采购或 Internet 使用访问字符串。</p></td>
</tr>
<tr class="even">
<td><p>Internet</p></td>
<td><p>xs:boolean</p></td>
<td><p>是</p></td>
<td><p>表示是否应为采购或 Internet 使用访问字符串。</p></td>
</tr>
<tr class="odd">
<td><p>AutoConnectOrder</p></td>
<td><p>xs:positiveinteger</p></td>
<td><p>否</p></td>
<td><p>确定 Windows 尝试连接到每个中 APNs 的顺序<a href="connectioninfolist.md" data-raw-source="[ConnectionInfoList](connectioninfolist.md)">ConnectionInfoList</a>元素。</p></td>
</tr>
<tr class="even">
<td><p>压缩</p></td>
<td><p>xs:token</p></td>
<td><p>否</p></td>
<td><p>指定是否将标头和数据传输使用的数据链接压缩。</p>
<p>值：启用或禁用</p></td>
</tr>
<tr class="odd">
<td><p>AuthProtocol</p></td>
<td><p>xs:token</p></td>
<td><p>否</p></td>
<td><p>指定用于激活 PDP 上下文的身份验证协议。</p>
<p>值：无、 PAP、 CHAP 中或 MsCHAPv2</p></td>
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
<td><p><a href="connectioninfolist.md" data-raw-source="[ConnectionInfoList](connectioninfolist.md)">ConnectionInfoList</a></p></td>
<td><p>APN 数据库中的运算符指定的详细信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


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

 

 





