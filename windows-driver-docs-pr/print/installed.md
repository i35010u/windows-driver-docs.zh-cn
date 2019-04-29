---
title: Installed (WSD)
description: Web Services for Devices (WSD) 已安装构造指示是否已安装与一组给定的条件相匹配的打印机功能。
ms.assetid: f05add2a-d37e-4eb5-8408-dd5eeef4b13c
keywords:
- 已安装的构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7940468d4083e31ffaee5c7dfd1ff6fa60a8dd6c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362761"
---
# <a name="installed-wsd"></a>Installed (WSD)


Web Services for Devices (WSD) 已安装构造指示是否已安装与一组给定的条件相匹配的打印机功能。 如果 XPath 筛选器获取有效的 XML 结果应用于给定的条件时，此算法返回 **，则返回 TRUE**。 已安装构造 WsdBidi.xsd 中定义。

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
<td><p>WSD 监视器将执行的查询的类型。</p></td>
</tr>
</tbody>
</table>

 

在 Windows 开始使用 Microsoft XML (MSXML) 2.6 中中, 实现的 XPath 语言提供的 XML 文件中指定元素的简便方法。 请参阅 Windows SDK 中的 XML 开发人员指南和[XPath 参考](https://go.microsoft.com/fwlink/p/?linkid=33165)有关详细信息。

已安装构造的行为取决于其父节点的定义。 如果不使用参数指定的已安装的构造，则查询时，将始终存在架构。 如果使用的参数使用指定的已安装的构造，则架构将在当前的 WSD 设备查询中找到相关联的参数值时才存在。 正在查询的软件必须能够处理这种情况，则不返回已安装架构。

已安装构造 WsdBidi.xsd 中定义。

### <a name="code-example"></a>代码示例

在下面的代码示例中，筛选器查找算法使用 XPath 查询来确认已安装硬盘。

```cpp
<Schema>
  <Property name='Printer'>
    <Property name='Configuration'>
      <Property name='HardDisk'>
        <Installed name='Installed'
            query='wprt:PrinterConfiguration'
            filter='wprt:PrinterConfiguration/wprt:Storage/wprt:StorageEntry[wprt:Type="HardDisk"]'/>
      </Property>
    </Property>
  </Property>
</Schema>
```

前面的示例生成以下查询：

```cpp
\Printer.Configuration.HardDisk:Installed
```

 

 




