---
title: Value (WSD)
description: 使用 WSD 值构造，可以通过从特定架构元素检索数据的查询来扩展双向通信架构。
ms.assetid: 8930e012-88ee-44ff-9abc-a15367f04ca3
keywords:
- 值构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c445047f91a382d2e9779db6ba52c770c59041cd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826994"
---
# <a name="value-wsd"></a>Value (WSD)


使用 WSD `Value` 构造，可以通过从 Web 服务接口中的特定架构元素检索数据的查询来扩展双向通信架构。

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
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>可有可无一个布尔值，指示端口监视器是否向驱动程序发送通知。 <strong>TRUE</strong>值指示端口监视器向驱动程序发送通知;<strong>FALSE</strong>表示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="even">
<td><p><strong>筛选器</strong></p></td>
<td><p>WSD 监视器将应用于查询所指定的 XML 文档的 XPath 查询。 请参阅本主题后面的讨论。</p></td>
</tr>
<tr class="odd">
<td><p><strong>名称</strong></p></td>
<td><p>架构值的名称。</p></td>
</tr>
<tr class="even">
<td><p>查询</p></td>
<td><p>WSD 监视器将执行的查询的类型。</p></td>
</tr>
<tr class="odd">
<td><p><strong>type</strong></p></td>
<td><p>中的数据类型 <code>Value</code> 构造， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type)"><strong>BIDI_TYPE</strong></a>枚举中的值。</p></td>
</tr>
<tr class="even">
<td><p><strong>xmllang</strong></p></td>
<td><p>可有可无一个布尔值，如果<strong>为 TRUE，则</strong>表示关联的 <code>Value</code> 构造应视为可本地化的字符串值。 这意味着，以上定义的 XPath 查询应返回由其 xml： lang 属性区分的节点列表。 然后，WSD 监视器将在值列表中搜索最佳区域设置匹配项。 默认值为<strong>FALSE</strong>。</p></td>
</tr>
</tbody>
</table>

 

XPath 语言是在 Windows 中实现的，提供了一种方便的方法来指定 XML 文件中的元素。 有关详细信息，请参阅 Windows SDK 和[XPath 参考](https://go.microsoft.com/fwlink/p/?linkid=33165)中的 XML 开发人员指南。

仅当 `Value` 构造的类型属性为 "双向\_STRING" 或 "双向\_文本" 时，才使用**xmllang**特性。

`Value` 构造是在 WsdBidi 中定义的。

### <a href="" id="example"></a>实例

在下面的代码示例中，WSD 监视器确定 RAM 内存的大小（以整数值的形式）。

```cpp
<Schema xmlns:nprt='http://schemas.microsoft.com/windows/2005/05/wdp/print'>
  <Property name='Printer'>
    <Property name='DeviceInfo'>
      <Value name='PrinterString' 
 query='nprt:PrinterDescription'
 filter='nprt:PrinterDescription/nprt:PrinterName' 
 type='BIDI_STRING' 
 xmllang='true'/>
    </Property>
    <Property name='Configuration'>
      <Property name='Memory'>
        <Value name='Size'
          query='wprt:PrinterConfiguration'
          filter='wprt:PrinterConfiguration/wprt:Storage/wprt:StorageEntry[wprt:Type="RAM"]/wprt:Size'
          type='BIDI_INT'/>
      </Property>
    </Property>
   </Property>
</Schema>
```

前面的示例将生成以下查询：

```cpp
\Printer.DeviceInfo:PrinterString
\Printer.Configuration.Memory:Size
```

 

 




