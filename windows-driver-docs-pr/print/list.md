---
title: 列表
description: 列表
ms.assetid: 4cf1c1ea-f890-4f9d-96ea-b79790f6bc60
keywords:
- 列表构造
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0131160bf7e15d6dfece9336d374f570ca4b9e66
ms.sourcegitcommit: d71024c0c782b5c013192d960700802eafc120f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84507100"
---
# <a name="list"></a>列表

Web Services for Devices （WSD） `List` 构造是一个字符串类型，用于撰写由 XPath 筛选器查询指定的值的逗号分隔列表。 `List`构造是在 WsdBidi 中定义的。

| 属性 | 说明 |
| --- | --- |
| **drvPrinterEvent** | 可有可无一个布尔值，指示端口监视器是否向驱动程序发送通知。 **TRUE**值指示端口监视器向驱动程序发送通知;**FALSE**表示端口监视器不向驱动程序发送通知。 |
| **筛选器** | WSD 监视器适用于查询指定的 XML 文档的 XPath 查询。 请参阅本主题后面的讨论。 |
| **name** | 架构值的名称。 |
| **query** | WSD 监视器执行的查询的类型。 |

从 Microsoft XML （MSXML）2.6 开始，在 Windows 中实现的 XPath 语言提供了一种在 XML 文件中指定元素的简便方法。 有关详细信息，请参阅[XPath 参考](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms256115(v=vs.100))。

`List`构造是在 WsdBidi 中定义的。

## <a name="code-example"></a>代码示例

在下面的代码示例中，以逗号分隔的列表为例，其中包含每个工作表中允许的最多页图像数，例如，"1，2，4"。

```xml
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

前面的示例将生成以下查询：

```console
\Printer.Layout.NumberUp.PagesPerSheet:Supported
```
