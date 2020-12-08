---
title: Converter
description: Converter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb224c3c73ec8a60bd9b58bc1897a959acedcb15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797517"
---
# <a name="converter"></a>Converter


使用 TCP/IP 转换器构造，可以通过从特定 MIB (SNMP 管理信息基础) 对象检索数据的查询来扩展 [双向通信](bidirectional-communication.md) 架构，然后将数据转换为基于在转换元素中指定的值对列表的字符串值。 转换器构造是在 Tcpbidi 中定义的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>deviceIndex</strong></p></td>
<td><p> (可选) 一个布尔值，如果该值 <strong>为 TRUE，则</strong>表示关联的算法必须包含指定 OID 中的设备索引;当此属性 <strong>为 FALSE</strong>时，将在 OID 后面追加一个尾随零。 默认值为 <strong>FALSE</strong>。 有关详细信息，请参阅此表后面的备注。</p></td>
</tr>
<tr class="even">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p> (可选) 一个布尔值，该值指示端口监视器是否向驱动程序发送通知。 <strong>TRUE</strong>值指示端口监视器向驱动程序发送通知;<strong>FALSE</strong>表示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p>一个表示架构元素名称的字符串值。</p></td>
</tr>
<tr class="even">
<td><p><strong>oid</strong></p></td>
<td><p>一个字符串值，表示 MIB 对象的地址，作为 (OID) 的对象 ID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p> (可选) 轮询间隔的整数值（以秒为单位）。 默认值为 600 秒。</p></td>
</tr>
<tr class="even">
<td><p><strong>useFirstIndex</strong></p></td>
<td><p> (可选) 可设置为读取 MIB 表中第一项的布尔值。 仅当转换器构造在属性实例中时，才使用此属性。</p></td>
</tr>
</tbody>
</table>

 

**注意**   支持 SNMP 协议的网络设备可以是不同 subdevices （如处理器、网络、打印机和磁盘存储）的主机。 在网络打印机中实现的 MIB 表包含按设备索引编制索引的条目。 若要从 MIB 表检索数据 (如输入纸盒) 的名称，该查询必须具有正确标识 subdevice 的设备索引。 标准 TCP/IP 端口监视器允许通过端口配置 UI 手动配置设备索引。 如果将 **deviceIndex** 特性设置为 **TRUE** ，则将生成具有适当设备索引的 OID，该索引是从端口配置 UI 获取的。 此外，如果转换器构造包含在属性实例中，并且缺少 **deviceIndex** 特性或将其设置为 **FALSE**，则 OID 的末尾将追加零个索引。

 

转换例程支持以下 MIB 数据类型：

INTEGER

Integer32

的 gauge32

Counter32

TimeTicks

Unsigned32

Counter64

半透明

八进制字符串

对象标识符

### <a name="conversion-element"></a><a href="" id="conversion-element"></a> 转换元素

每个转换器构造都包含一个或多个转换元素，用于定义从 MIB 元素读入双向架构值的值的映射。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>mibValue</p></td>
<td><p> (可选) 一个字符串值，该值表示可以从 MIB 中读取的一个可能的数据值。</p></td>
</tr>
<tr class="even">
<td><p>bidiValue</p></td>
<td><p> (可选) 一个字符串值，该值表示在数据与此转换元素的 <strong>mibValue</strong> 特性匹配时返回的双向值。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a><a href="" id="code-example"></a> 代码示例

下面的代码示例通过添加新的属性和转换器构造来扩展双向通信架构。

```cpp
<Property name="Printer">
  <Property name="Layout">
    <Property name="InputBins">
      <IndexedProperty name="Bin">
        <Converter name="BinType" oid="1.3.6.1.2.1.43.8.2.1.2" deviceIndex="true">
          <Conversion mibValue="2" bidiValue="Unknown"/>
          <Conversion mibValue="3" bidiValue="SheetFeedAutoRemoveableTray"/>
          <Conversion mibValue="4" bidiValue="SheetFeedAutoNonRemovableTray"/>
          <Conversion mibValue="5" bidiValue="SheetFeedManual"/>
          <Conversion mibValue="6" bidiValue="ContinuousRoll"/>
          <Conversion mibValue="7" bidiValue="ContinuousFanFold"/>
        </Converter>
      </IndexedProperty>
    </Property>
    <Property name="Orientation">
      <Converter name="CurrentValue" oid="1.3.6.1.2.1.43.15.1.1.7" deviceIndex="true" useFirstIndex="true">
        <Conversion mibValue="3" bidiValue="Portrait"/>
        <Conversion mibValue="4" bidiValue="Landscape"/>
     </Converter>
   </Property>
 </Property>
 <Property name="Custom">
    <Property name="HostRescourceMIB">
      <Converter name="InterfaceName" oid="1.3.6.1.2.1.2.1">
      <Conversion mibValue="1" bidiValue="InterfaceOne"/>
    <Conversion mibValue="2" bidiValue="InterfaceTwo"/>
     </Converter>
  </Property>
 </Property
</Property>
```

前面的示例将生成以下查询。

```cpp
\Printer.Layout.InputBins.Bin###:BinType
\Printer.Layout.Orientation:CurrentValue
\Printer.Custom.HostResourceMIB:InterfaceName
```

的转换器构造 `BinType` 包含在 IndexedProperty 实例中，因此，当前 MIB 表行条目会自动追加到 OID 上。

由于的转换器构造 `CurrentValue ` 包含在属性实例中，并且 **useFirstIndex** 特性设置为 "true"，因此会自动向 OID 追加尾随 "1"。

的转换器构造 `InterfaceName` 包含在属性实例中，因此尾随零会自动追加到 OID 上。

 

 




