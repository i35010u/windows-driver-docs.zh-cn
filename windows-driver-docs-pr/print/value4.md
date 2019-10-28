---
title: Value (TCP/IP)
description: TCP/IP 值构造允许使用从特定 MIB 对象检索数据的查询来扩展双向通信架构。
ms.assetid: 46b24830-10a1-405b-9c12-b5804f76d668
keywords:
- 值构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b21c9ac36ddbb26590bea0d3f194e2a0fc6d72b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840398"
---
# <a name="value-tcpip"></a>Value (TCP/IP)


使用 TCP/IP `Value` 构造，可以通过从特定 MIB 对象检索数据的查询来扩展双向通信架构。 `Value` 构造是在 Tcpbidi 中定义的。

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
<td><p>一个标志，如果<strong>为 TRUE，则</strong>表示关联的算法必须包含指定 OID 中的设备索引;<strong>为 FALSE</strong>时，将在 OID 后面追加一个尾随零。 默认值为<strong>FALSE</strong>。 有关详细信息，请参阅此表后面的说明。</p></td>
</tr>
<tr class="even">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>可有可无一个布尔值，指示端口监视器是否向驱动程序发送通知。 <strong>TRUE</strong>值指示端口监视器向驱动程序发送通知;<strong>FALSE</strong>表示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="odd">
<td><p><strong>名称</strong></p></td>
<td><p>架构值的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>oid</strong></p></td>
<td><p>MIB 对象的地址，作为对象 ID （OID）。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>可有可无轮询间隔的值（以秒为单位）。 默认值为600秒。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p><code> Value</code> 构造中的数据类型（ <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type)"><strong>BIDI_TYPE</strong></a>枚举中的值）。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  支持 SNMP 协议的网络设备可以是不同 subdevices （如处理器、网络、打印机和磁盘存储）的主机。 网络打印机中实现的 MIB 表包含按设备索引编制索引的条目。 为了检索 MIB 表中的数据（如输入纸盒的名称），该查询必须具有正确标识 subdevice 的设备索引。 标准 TCP/IP 端口监视器允许通过端口配置 UI 手动配置设备索引。 使用**deviceIndex**= "true" 的双向扩展会生成一个 OID，其中包含从端口配置 UI 获取的适当的设备索引。 此外，如果 `Value` 构造包含在属性实例中，则 OID 的末尾将追加零个索引。

 

### <a href="" id="code-example"></a>代码示例

下面的代码示例通过向**Printer**属性添加新的属性 "**系统**" 来扩展双向通信架构。 **系统**属性具有 `Value` 的构造，其**名称**、**类型**和**oid**特性均为。

```cpp
<Property name="Printer">
  <Property name="System">
    <Value name="Name" type="BIDI_STRING" oid="1.3.6.1.2.1.1.5"/>
  </Property>
</Property>
```

前面的示例将生成以下查询：

```cpp
\Printer.System:Name
```

请注意，因为 `Value` 构造包含在属性实例中，而不是包含在 IndexedProperty 实例中，所以会自动向 OID 追加一个尾随零。

 

 




