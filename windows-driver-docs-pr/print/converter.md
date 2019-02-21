---
title: Converter
description: Converter
ms.assetid: eadbbaf5-3fe3-484f-b3f1-3d543ddc817f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 662846dc5874f362c4a26852ffc9b411212f44b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544496"
---
# <a name="converter"></a>Converter


TCP/IP 转换器构造使您能够扩展[bidi 通信](bidirectional-communication.md)架构的查询，从特定的 MIB （SNMP 管理信息库） 对象中检索数据，然后将数据转换为字符串值根据转换元素中指定的值对的列表。 转换器构造 Tcpbidi.xsd 中定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>deviceIndex</strong></p></td>
<td><p>（可选）一个布尔值，当<strong>，则返回 TRUE</strong>，表示关联的算法，必须在指定的 OID; 包含设备索引时此特性<strong>FALSE</strong>，尾随零追加到该 OID。 默认值是<strong>FALSE</strong>。 有关详细信息，请参阅此表后面的说明。</p></td>
</tr>
<tr class="even">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>（可选）一个布尔值，该值指示端口监视器是否将通知发送到该驱动程序。 一个<strong>，则返回 TRUE</strong>值指示端口监视器将通知发送到驱动程序;<strong>FALSE</strong>指示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="odd">
<td><p><strong>名称</strong></p></td>
<td><p>一个字符串值，该值表示此架构元素的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>oid</strong></p></td>
<td><p>一个字符串值，该值表示 MIB 对象的地址为对象 ID (OID)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>（可选）轮询间隔 （秒） 的一个整数值。 默认值为 600 秒。</p></td>
</tr>
<tr class="even">
<td><p><strong>useFirstIndex</strong></p></td>
<td><p>（可选）一个布尔值，可设置为读取 MIB 表中的第一个条目。 仅当转换器构造是中的属性实例时，才使用此属性。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  支持 SNMP 协议的网络设备可以是不同的子设备，如处理器、 网络、 打印机和磁盘存储的主机。 在网络打印机中实现的 MIB 表中具有由设备索引编制索引的条目。 若要从 MIB 表 （如送纸器的名称） 检索数据，查询必须正确地标识子设备索引。 标准 TCP/IP 端口监视器允许通过端口配置 UI 来手动配置的设备索引。 使用扩展名为 bidi **deviceIndex**属性设置为**TRUE**生成具有适当的设备索引从端口配置 UI 获取 OID。 此外，如果转换器构造包含中的属性实例和**deviceIndex**特性缺少或设置为**FALSE**，OID 会追加到其最终的零的索引。

 

支持以下 MIB 数据类型转换例程：

INTEGER

Integer32

Gauge32

Counter32

TimeTicks

Unsigned32

Counter64

不透明

八位字节字符串

对象标识符

### <a href="" id="conversion-element"></a> 转换元素

每个转换器构造将包括一个或多个转换元素可定义从 MIB 元素读取到 Bidi 架构值的值的映射。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>mibValue</p></td>
<td><p>（可选）一个字符串值，该值表示无法从 MIB 中读取的一个可能的数据值。</p></td>
</tr>
<tr class="even">
<td><p>bidiValue</p></td>
<td><p>（可选）一个字符串值，表示 bidi 值，如果数据与相匹配，则返回该值<strong>mibValue</strong>此转换元素的属性...</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="code-example"></a> 代码示例

下面的代码示例通过添加新属性扩展的双向通信架构和转换器构造。

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

前面的示例生成下面的查询。

```cpp
\Printer.Layout.InputBins.Bin###:BinType
\Printer.Layout.Orientation:CurrentValue
\Printer.Custom.HostResourceMIB:InterfaceName
```

转换器构造`BinType`包含 IndexedProperty 实例中，因此，当前 MIB 表行条目会自动附加到 OID。

因为为构造转换器`CurrentValue `了属性实例中包含和**useFirstIndex**属性设置为"true"，尾随"1"会自动追加到该 OID。

转换器构造`InterfaceName`包含在一个属性的实例，因此自动追加到该 OID 尾随零。

 

 




