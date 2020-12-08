---
title: Installed (TCP/IP)
description: TCP/IP 已安装的构造包含 MIB 表的行 (OID) 的对象 ID，以及查找值的列表。
keywords:
- 已安装构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7322ae035babbb8eaa109fb7f13b5d4611521b85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835689"
---
# <a name="installed-tcpip"></a>Installed (TCP/IP)


TCP/IP 已安装的构造包含 MIB 表的行 (OID) 的对象 ID，以及查找值的列表。 如果行中存在任意查找值，则该算法将返回 **TRUE**。 与打印机配置相关的大多数查询都应该确定是否有特定值存储在打印机的 MIB 中，然后返回布尔值结果。 已安装的构造是在 Tcpbidi 中定义的。

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
<td><p> (Optional) 标志，如果 <strong>为 TRUE，则</strong>意味着关联的算法必须包含指定 OID 中的设备索引; <strong>为 FALSE</strong>时，将在 OID 后面追加一个尾随零。 默认值为 <strong>FALSE</strong>。 有关详细信息，请参阅 " <a href="value.md" data-raw-source="[Value](value.md)">值</a>" 页上的说明。</p></td>
</tr>
<tr class="even">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p> (可选) 一个布尔值，该值指示端口监视器是否向驱动程序发送通知。 <strong>TRUE</strong>值指示端口监视器向驱动程序发送通知;<strong>FALSE</strong>表示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p>架构值的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>oid</strong></p></td>
<td><p>作为 OID 的 MIB 表的行。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>轮询间隔的值（以秒为单位）。 默认值为 600 秒。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>代码示例

在下面的代码示例中，lookup 算法从1.3.6.1.2.1.43.13.4.1.9 中检索 MIB 表行。 &lt;**deviceIndex** &gt; 。 如果此表行包含3个或4个，则查询返回 **TRUE**;否则，查询将返回 **FALSE**。

```cpp
<Property name="DuplexUnit">
  <Installed name="Installed" oid="1.3.6.1.2.1.43.13.4.1.9" deviceIndex="true">
    <Lookup value="3"/>
    <Lookup value="4"/>
  </Installed>
</Property>
```

前面的示例将生成以下查询：

```cpp
\Printer.Configuration.DuplexUnit:Installed
```

 

 




