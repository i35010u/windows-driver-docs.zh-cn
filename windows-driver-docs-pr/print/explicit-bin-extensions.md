---
title: 显式 Bin 扩展
description: 显式 Bin 扩展
ms.assetid: a9f7f290-1af8-4312-b348-c1c98a3fc4a6
keywords:
- 显式 bin 扩展 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 780b1885393e758c31af70b018e649a09a5ffdbc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843124"
---
# <a name="explicit-bin-extensions"></a>显式 Bin 扩展


您可以使用特殊构造**BinValue**进一步扩展隐式 bin 扩展。 此对象确定 prtInputTable 或 prtOutputTable 表中的哪个 MIB 对象包含新的数据。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type)"><strong>BIDI_TYPE</strong></a>枚举中的枚举器。</p></td>
</tr>
<tr class="odd">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>可有可无一个布尔值，指示端口监视器是否向驱动程序发送通知。 <strong>TRUE</strong>值指示端口监视器向驱动程序发送通知;<strong>FALSE</strong>表示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="even">
<td><p><strong>valueId</strong></p></td>
<td><p>Printmib. prtInput. prtInputTable. prtInputEntry 中的 MIB 对象。<strong>valueId</strong> （input bin）或 Printmib. PrtOutput. PrtOutputTable. prtOutputEntry。<strong>valueId</strong> （输出箱）。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>代码示例

下面的代码示例演示如何使用**BinValue**构造来添加新的属性，即**安全性**。 这可以扩展隐式 bin 扩展。

```cpp
<Property name="Layout">
  <Property name="InputBins">
    <InputBin name="TopBin" mibName="TRAY 1">
      <BinValue name="Security" type="BIDI_INT" valueId="19"/>
    </InputBin>
  </Property>
</Property>
```

前面的示例将生成以下查询：

```cpp
\Printer.Layout.InputBins.TopBin:Security
```

下面的代码示例演示如何使用**BinValue**构造来添加状态值。 如前面的示例所示，这具有扩展隐式 bin 扩展的效果。

```cpp
<Property name="Finishing">
  <Property name="OutputBins">
    <OutputBin name="TopBin" mibName="STANDARD BIN">
       <BinValue name="Status" type="BIDI_INT" valueId="6"/>
    </OutputBin>
  </Property>
</Property>
```

前面的示例将生成以下查询：

```cpp
\Printer.Finishing.OutputBins.TopBin:Status
```

 

 




