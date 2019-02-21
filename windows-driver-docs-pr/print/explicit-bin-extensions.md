---
title: 显式 Bin 扩展
description: 显式 Bin 扩展
ms.assetid: a9f7f290-1af8-4312-b348-c1c98a3fc4a6
keywords:
- 显式 bin 扩展 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fb04bc70c3d677467e1efea12f77b9e5baed246
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519921"
---
# <a name="explicit-bin-extensions"></a>显式 Bin 扩展


您可以通过使用特殊构造，进一步扩展的隐式 bin 扩展**BinValue**。 此对象确定 prtInputTable 或 prtOutputTable 表内的 MIB 对象包含的新数据。

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
<td><p><strong>名称</strong></p></td>
<td><p>Bin 的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p>中的枚举器<a href="https://msdn.microsoft.com/library/windows/hardware/ff545211" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545211)"> <strong>BIDI_TYPE</strong> </a>枚举。</p></td>
</tr>
<tr class="odd">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>（可选）一个布尔值，该值指示端口监视器是否将通知发送到该驱动程序。 一个<strong>，则返回 TRUE</strong>值指示端口监视器将通知发送到驱动程序;<strong>FALSE</strong>指示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="even">
<td><p><strong>valueId</strong></p></td>
<td><p>在任一 printmib.prtInput.prtInputTable.prtInputEntry MIB 对象。<strong>valueId</strong> （纸盒） 或 printmib.prtOutput.prtOutputTable.prtOutputEntry。<strong>valueId</strong> (输出 bin)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>代码示例

下面的代码示例演示如何**BinValue**构造可用于将新属性，添加**安全**。 扩展的隐式 bin 扩展效果。

```cpp
<Property name="Layout">
  <Property name="InputBins">
    <InputBin name="TopBin" mibName="TRAY 1">
      <BinValue name="Security" type="BIDI_INT" valueId="19"/>
    </InputBin>
  </Property>
</Property>
```

前面的示例生成以下查询：

```cpp
\Printer.Layout.InputBins.TopBin:Security
```

下面的代码示例演示如何**BinValue**构造可用于添加将 Status 值。 在前面的示例中，此操作将扩展的隐式 bin 扩展。

```cpp
<Property name="Finishing">
  <Property name="OutputBins">
    <OutputBin name="TopBin" mibName="STANDARD BIN">
       <BinValue name="Status" type="BIDI_INT" valueId="6"/>
    </OutputBin>
  </Property>
</Property>
```

前面的示例生成以下查询：

```cpp
\Printer.Finishing.OutputBins.TopBin:Status
```

 

 




