---
title: Installed (WSD)
description: " (WSD) 已安装的 \"用于设备的 Web 服务\" 构造指示是否已安装与一组给定条件相匹配的打印机功能。"
ms.assetid: f05add2a-d37e-4eb5-8408-dd5eeef4b13c
keywords:
- 已安装构造
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0e2f16d57da0dee609813014909312e8c774d33e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217955"
---
# <a name="installed-wsd"></a>Installed (WSD)

 (WSD) 已安装的 "用于设备的 Web 服务" 构造指示是否已安装与一组给定条件相匹配的打印机功能。 如果 XPath 筛选器在应用于给定条件时获得有效的 XML 结果，则此算法将返回 **TRUE**。 已安装的构造是在 WsdBidi 中定义的。

| Attribute | 说明 |
| --- | --- |
| **drvPrinterEvent** |  (可选) 一个布尔值，该值指示端口监视器是否向驱动程序发送通知。 **TRUE**值指示端口监视器向驱动程序发送通知;**FALSE**表示端口监视器不向驱动程序发送通知。 |
| **filter** | WSD 监视器适用于查询指定的 XML 文档的 XPath 查询。 请参阅本主题后面的讨论。 |
| name  | 架构值的名称。 |
| **query** | WSD 监视器将执行的查询的类型。 |

从 Microsoft XML (MSXML) 2.6 开始，在 Windows 中实现的 XPath 语言为指定 XML 文件中的元素提供了一种简便方法。 有关详细信息，请参阅 [XPath 参考](/previous-versions/dotnet/netframework-4.0/ms256115(v=vs.100)) 。

已安装的构造的行为取决于其父节点的定义。 如果在未使用参数的情况下指定了安装的构造，则在查询时，架构将始终存在。 如果使用参数指定了已安装的构造，则仅当在当前 WSD 设备查询中找到关联的参数值时，架构才会存在。 进行查询的软件必须能够处理未返回已安装架构的情况。

已安装的构造是在 WsdBidi 中定义的。

## <a name="code-example"></a>代码示例

在下面的代码示例中，筛选器查找算法使用 XPath 查询来确认是否安装了硬盘。

```xml
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

前面的示例将生成以下查询：

```cpp
\Printer.Configuration.HardDisk:Installed
```