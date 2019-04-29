---
title: 输入和输出 Bin 的 TCP/IP 架构扩展
description: 输入和输出 Bin 的 TCP/IP 架构扩展
ms.assetid: 942325e8-588c-4171-91fa-366db6e2cb16
keywords:
- TCP/IP 架构扩展 WDK 打印机
- 架构扩展 WDK TCP/IP
- OutputBin 构造
- InputBin 构造
- 输出收集箱 WDK 打印机
- 输入的箱 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 720e096a4e2615098f74c011d0f813385dcddd47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388063"
---
# <a name="tcpip-schema-extensions-for-input-and-output-bins"></a>输入和输出 Bin 的 TCP/IP 架构扩展


Tcpbidi.xsd 文件，它用于扩展 bidi 架构定义了两个构造，InputBin 和 OutputBin，实现与特定的打印机相关的扩展的输入和输出箱。InputBin 和 OutputBin 构造这两个具有以下可用的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>名称</strong></p></td>
<td><p>Bin bidi 架构名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>mibName</strong></p></td>
<td><p>Bin MIB 名称。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>（可选）轮询间隔 （秒） 的值。 默认值为 600 秒。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>代码示例

下面的代码示例显示了如何 InputBin 和 OutputBin 构造可用于确定两个输入的箱和一个输出 bin。

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

[特定于驱动程序的箱](driver-specific-bins.md)

 

 




