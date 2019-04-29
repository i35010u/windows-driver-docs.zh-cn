---
title: 列表
description: 列表
ms.assetid: 4cf1c1ea-f890-4f9d-96ea-b79790f6bc60
keywords:
- 列表构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9504c0a185eec59f7eab3593153eec0d00b67a26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388085"
---
# <a name="list"></a>列表


Web Services for Devices (WSD)`List`构造是字符串类型，它将指定的 XPath 筛选器查询的值的以逗号分隔列表。 `List` WsdBidi.xsd 中定义构造。

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
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>（可选）一个布尔值，该值指示端口监视器是否将通知发送到该驱动程序。 一个<strong>，则返回 TRUE</strong>值指示端口监视器将通知发送到驱动程序;<strong>FALSE</strong>指示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="even">
<td><p><strong>filter</strong></p></td>
<td><p>WSD 监视器将适用于查询指定的 XML 文档中的 XPath 查询。 请参阅本主题后面讨论。</p></td>
</tr>
<tr class="odd">
<td><p><strong>名称</strong></p></td>
<td><p>架构值的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>查询</strong></p></td>
<td><p>WSD 监视器执行的查询的类型。</p></td>
</tr>
</tbody>
</table>

 

在 Windows 开始使用 Microsoft XML (MSXML) 2.6 中中, 实现的 XPath 语言提供的 XML 文件中指定元素的简便方法。 请参阅 Windows SDK 中的 XML 开发人员指南和[XPath 参考](https://go.microsoft.com/fwlink/p/?linkid=33165)有关详细信息。

`List` WsdBidi.xsd 中定义构造。

### <a name="code-example"></a>代码示例

在下面的代码示例中，以逗号分隔的列表由组成，其中包含允许的每张多打印，例如"1,2,4"页的页面图像数。

```cpp
<Property name='Layout'>
  <Property name='NumberUp'>
    <Property name='PagesPerSheet'>
      <List name='Supported
        query='wprt:PrinterCapabilities'
        filter='wprt:PrinterCapabilites/wprt:JobValues/wprt:DocumentProcessing/wprt:NumberUp/wprt:NUpPagesPerSheet/wprt:AllowedValue'/>
    </Property>
  </Property>
</Property>
```

前面的示例生成以下查询：

```cpp
\Printer.Layout.NumberUp.PagesPerSheet:Supported
```

 

 




