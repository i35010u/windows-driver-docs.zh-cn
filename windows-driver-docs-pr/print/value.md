---
title: 值 (WSD)
description: WSD 值构造可以双向通信使用扩展架构从特定架构元素中检索数据的查询。
ms.assetid: 8930e012-88ee-44ff-9abc-a15367f04ca3
keywords:
- 值构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92dda2e223f51cf507b07411db7d51d8f227255d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546858"
---
# <a name="value-wsd"></a>值 (WSD)


WSD`Value`构造可以进行扩展使用从 Web 服务接口中的特定架构元素中检索数据的查询的双向通信架构。

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
<td><p>（可选）一个布尔值，该值指示端口监视器是否将通知发送到该驱动程序。 一个<strong>，则返回 TRUE</strong>值指示端口监视器将通知发送到驱动程序;<strong>FALSE</strong>指示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="even">
<td><p><strong>filter</strong></p></td>
<td><p>WSD 监视器将应用于查询指定的 XML 文档中的 XPath 查询。 请参阅本主题后面讨论。</p></td>
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
<td><p>中的数据类型 <code>Value</code> 构造中的值<a href="https://msdn.microsoft.com/library/windows/hardware/ff545211" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545211)"> <strong>BIDI_TYPE</strong> </a>枚举。</p></td>
</tr>
<tr class="even">
<td><p><strong>xmllang</strong></p></td>
<td><p>（可选）一个布尔值，当<strong>，则返回 TRUE</strong>，意味着关联 <code>Value</code> 构造应视为可本地化的字符串值。 这意味着，上面定义的 XPath 查询应返回的区别在于其 xml: lang 属性的不同节点的列表。 WSD 监视器然后将搜索最佳的区域设置匹配的值的列表。 默认值是<strong>FALSE</strong>。</p></td>
</tr>
</tbody>
</table>

 

XPath 语言在 Windows 中实现，并提供的 XML 文件中指定元素的简便方法。 请参阅 Windows SDK 中的 XML 开发人员指南和[XPath 参考](https://go.microsoft.com/fwlink/p/?linkid=33165)有关详细信息。

**Xmllang**使用属性时，才的类型属性`Value`构造可以是"BIDI\_字符串"或"BIDI\_文本"。

`Value` WsdBidi.xsd 中定义构造。

### <a href="" id="example"></a> 示例

在下面的代码示例中，WSD 监视器确定的大小，为整数值，RAM 内存。

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

前面的示例生成以下查询：

```cpp
\Printer.DeviceInfo:PrinterString
\Printer.Configuration.Memory:Size
```

 

 




