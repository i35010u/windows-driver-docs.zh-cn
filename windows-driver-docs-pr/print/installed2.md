---
title: Installed (TCP/IP)
description: 安装 tcp/ip 协议构造包含的对象 ID (OID) 的 MIB 表的行和查找值的列表。
ms.assetid: 4e14d8c1-7c66-4035-845d-f3f92dad8c4f
keywords:
- 已安装的构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc940e2b3b5d5f40cf0ddd587281c3782a976de2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362863"
---
# <a name="installed-tcpip"></a>Installed (TCP/IP)


安装 tcp/ip 协议构造包含的对象 ID (OID) 的 MIB 表的行和查找值的列表。 如果查找值的任何存在的行中，此算法返回 **，则返回 TRUE**。 配置打印机相关的大多数查询应确定是否存在特定的值存储在打印机的 MIB，然后返回结果为布尔值。 已安装构造 Tcpbidi.xsd 中定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>deviceIndex</strong></p></td>
<td><p>（可选）一个标志，当<strong>，则返回 TRUE</strong>，表示关联的算法，必须在指定的 OID; 包含设备索引时<strong>FALSE</strong>，尾随零追加到该 OID。 默认值是<strong>FALSE</strong>。 有关详细信息，请参阅 》 的页上的说明<a href="value.md" data-raw-source="[Value](value.md)">值</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>（可选）一个布尔值，该值指示端口监视器是否将通知发送到该驱动程序。 一个<strong>，则返回 TRUE</strong>值指示端口监视器将通知发送到驱动程序;<strong>FALSE</strong>指示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="odd">
<td><p><strong>名称</strong></p></td>
<td><p>架构值的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>oid</strong></p></td>
<td><p>作为 OID 的 MIB 表的行。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>轮询间隔 （秒） 的值。 默认值为 600 秒。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>代码示例

在下面的代码示例中，查找算法从 1.3.6.1.2.1.43.13.4.1.9 检索 MIB 表行。&lt; **deviceIndex**&gt;。 如果此表行包含 3 或 4，查询将返回 **，则返回 TRUE**; 否则为该查询将返回**FALSE**。

```cpp
<Property name="DuplexUnit">
  <Installed name="Installed" oid="1.3.6.1.2.1.43.13.4.1.9" deviceIndex="true">
    <Lookup value="3"/>
    <Lookup value="4"/>
  </Installed>
</Property>
```

前面的示例生成以下查询：

```cpp
\Printer.Configuration.DuplexUnit:Installed
```

 

 




