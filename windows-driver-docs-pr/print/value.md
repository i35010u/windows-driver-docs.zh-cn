---
title: Value (WSD)
description: 使用 WSD 值构造，可以通过从特定架构元素检索数据的查询来扩展双向通信架构。
ms.assetid: 8930e012-88ee-44ff-9abc-a15367f04ca3
keywords:
- 值构造
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 92ddd4ac96518272be242686320f44cfc796ed54
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211879"
---
# <a name="value-wsd"></a>Value (WSD)

使用 WSD `Value` 构造，可以通过从 Web 服务接口中的特定架构元素检索数据的查询来扩展双向通信架构。

| Attribute | 说明 |
|--|--|
| **drvPrinterEvent** |  (可选) 一个布尔值，该值指示端口监视器是否向驱动程序发送通知。 **TRUE**值指示端口监视器向驱动程序发送通知;**FALSE**表示端口监视器不向驱动程序发送通知。 |
| **filter** | WSD 监视器将应用于查询所指定的 XML 文档的 XPath 查询。 请参阅本主题后面的讨论。 |
| name  | 架构值的名称。 |
| **query** | WSD 监视器将执行的查询的类型。 |
| **type** | 构造中的数据类型 `Value` ， [**BIDI_TYPE**](/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type) 枚举中的值。 |
| **xmllang** |  (可选) 一个布尔值，如果该值 **为 TRUE，则**表示 `Value` 应将关联构造作为可本地化字符串值处理。 这意味着，以上定义的 XPath 查询应返回由其 xml： lang 属性区分的节点列表。 然后，WSD 监视器将在值列表中搜索最佳区域设置匹配项。 默认值为 **FALSE**。 |

XPath 语言是在 Windows 中实现的，提供了一种方便的方法来指定 XML 文件中的元素。 有关详细信息，请参阅 [XPath 参考](/previous-versions/dotnet/netframework-4.0/ms256115(v=vs.100)) 。

仅**xmllang**当构造的类型属性 `Value` 为 "双向 \_ 字符串" 或 "双向文本" 时，才使用 xmllang 属性 \_ 。

`Value`构造是在 WsdBidi 中定义的。

## <a name="example"></a>示例

在下面的代码示例中，WSD 监视器确定 RAM 内存的大小（以整数值的形式）。

```xml
<Schema xmlns:nprt='https://schemas.microsoft.com/windows/2005/05/wdp/print'>
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

```console
\Printer.DeviceInfo:PrinterString
\Printer.Configuration.Memory:Size
```