---
title: 输入和输出 Bin 的 TCP/IP 架构扩展
description: 输入和输出 Bin 的 TCP/IP 架构扩展
keywords:
- TCP/IP 架构扩展 WDK 打印机
- 架构扩展 WDK TCP/IP
- OutputBin 构造
- InputBin 构造
- 输出箱 WDK 打印机
- 输入箱 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1f0aeb6d535b7fbe34bc9ff9a47aa73a97e9d46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806751"
---
# <a name="tcpip-schema-extensions-for-input-and-output-bins"></a>输入和输出 Bin 的 TCP/IP 架构扩展


用于扩展双向架构的 Tcpbidi 文件定义了两个构造 InputBin 和 OutputBin，它们实现了与特定打印机输入和输出容器相关的扩展。InputBin 和 OutputBin 构造都具有以下可用属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>name</p></td>
<td><p>Bin 的双向架构名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>mibName</strong></p></td>
<td><p>Bin 的 MIB 名称。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p> (可选) 轮询间隔的值（以秒为单位）。 默认值为 600 秒。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>代码示例

下面的代码示例演示了如何使用 InputBin 和 OutputBin 构造来识别两个输入箱和一个输出箱。

```cpp
<Property name="Printer">
  <Property name="Layout">
    <Property name="InputBins">
      <InputBin name="TopBin"    mibName="TRAY 1"/>
      <InputBin name="BottomBin" mibName="TRAY 2"/>
    </Property>
  </Property>
  <Property name="Finishing">
    <Property name="OutputBins">
      <OutputBin name="TopBin" mibName="STANDARD BIN"/>
    </Property>
  </Property>
</Property>
```

本部分包括以下主题。

[隐式 Bin 扩展](implicit-bin-extensions.md)

[显式 Bin 扩展](explicit-bin-extensions.md)

[驱动程序特定的 Bin](driver-specific-bins.md)

 

 




