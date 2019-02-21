---
title: 标准 XPS 筛选器
description: Windows 提供了两个 （标准） XPS 筛选器以支持内置转换从 XPS PCL6 和 PostScript 级别 3。
ms.assetid: 6404D215-8154-4604-A67B-19B20D1CF229
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a20e14a5ae9b49553276a46b64b1b27766fe16f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519132"
---
# <a name="standard-xps-filters"></a>标准 XPS 筛选器


Windows 提供了两个 （标准） XPS 筛选器以支持内置转换从 XPS PCL6 和 PostScript 级别 3。

Windows 提供的筛选器是可用于打印类驱动程序和特定于模型的 v4 打印驱动程序。 可以与 IHV 功能筛选器，以及 IHV 后期处理筛选器组合这些 XPS 筛选器，根据需要以确保与现有的固件实现兼容性。

**请注意**提供这些 Windows XPS 筛选器不是可重新分发，且不支持到 v3 打印驱动程序。



## <a name="the-manifest-file"></a>清单文件


若要使用 Windows 提供 XPS 筛选器，v4 驱动程序清单文件必须使用的下，RequiredFiles 指令**DriverConfig**部分，以指定的筛选器。 这些是筛选器的名称：

*MSxpsPCL6.dll*。 提供从 XPS 到 PCL6 转换。
*MSxpsPS.dll*。 提供从 XPS 转换为 PostScript 级别 3。
不支持重新分发和没有 INF 更新所需的这些筛选器，一个。
## <a name="print-filter-pipeline-configuration"></a>打印筛选器管道配置


若要配置要使用这些筛选器的打印筛选器管道，必须创建配置文件，如以下示例所示。

指定到 PCL6 转换的示例配置文件。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Filters>
  <Filter dll="MSxpsPCL6.dll" clsid="{3821E518-33AF-4d17-92B3-28EB410D46B6}" name="Microsoft XPS to PCL6">
    <Input guid="{4d47a67c-66cc-4430-850e-daf466fe5bc4}" comment="IID_IPrintReadStream" />
    <Output guid="{65bb7f1b-371e-4571-8ac7-912f510c1a38}" comment="IID_IPrintWriteStream" />
  </Filter>  
</Filters>
```

指定 PostScript 到转换的示例配置文件。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Filters>
  <Filter dll="MSxpsPS.dll" clsid="{8636D90A-5E03-4d62-9269-E06493C57473}" name="Microsoft XPS to PS">
    <Input guid="{4d47a67c-66cc-4430-850e-daf466fe5bc4}" comment="IID_IPrintReadStream" />
    <Output guid="{65bb7f1b-371e-4571-8ac7-912f510c1a38}" comment="IID_IPrintWriteStream" />
  </Filter>  
</Filters>
```

## <a name="supported-features"></a>支持的功能


标准 XPS 筛选器都支持许多通用功能。 所有功能定义驱动程序都使用 GPD 或 PPD 文件。 *MSxpsPCL6.dll*筛选器要求 GPD 文件的使用进行配置，并*MSxpsPS.dll*筛选器要求 PPD 文件的使用进行配置。 除非另行说明，如果自定义的 PDL 命令指定的一项功能，将使用它。

如果在任何特定部分下存在注入字符串 (与指定**\*顺序**命令)，然后在 GPD 文件的情况下筛选器将进行各种假设这些字符串的内容，并将避免发送默认命令。 这是因为发送默认命令在这种情况下可能导致命令发生冲突。 因此 GPD 文件的创建者必须遵循以下准则：

-   作业\_安装程序。\# o PCL6 二进制 Stream 标头 (例如:")&lt;SP&gt;HP PCL XL; 1;&lt;CR&gt;&lt;LF&gt;") 必须存在。
    必须存在 o BeginSession 运算符，包括所有必需的属性。
    必须存在 o OpenDataSource 运算符，包括所有必需的属性。
-   页\_安装程序。\# o BeginPage 运算符必须存在，其中包括所需的所有属性。
-   页\_完成。\# o EndPage 运算符必须存在。
-   作业\_完成。\# o CloseDataSource 运算符必须存在。
    o EndSession 运算符必须存在。
    o EndPJLCommands 运算符必须存在。

XPS 标准筛选器生成相应的 PDL 数据设置页上，根据原点\*PrintableArea， \*PrintableOrigin 或\*ImageableArea 命令。 为避免出现于预期的来源的其他偏移量，GPD 文件不应指定任何和 = SetPageOrigin 命令\*Cmd 其纸张大小的字符串定义。

有关支持的标准 XPS 筛选器，请参阅 PrintTicket 功能的详细信息[支持的 PrintTicket 功能](supported-printticket-features.md)。

## <a name="retrieving-printticket-in-post-processing-filters"></a>在后期处理筛选器检索 PrintTicket


一个 MSxps 筛选器后添加后续处理筛选器时发布与 Windows 8 的 v4 驱动程序模型，有时还不得不添加预处理的筛选器。 添加预处理的筛选器是为了捕获作业级别的打印票证所必需的。 但这种方法实质上是添加一个对象的基于模型的筛选器，一个基于流的 MSxps 筛选器，从而导致反序列化，然后再打印的数据，只需提取 PrintTicket 的序列化之前。

在 Windows 8.1，用户默认 PrintTicket 与 MSxps 筛选器，在作业级别 PrintTicket 和合并的 PrintTicket 合并然后添加到打印筛选器管道的属性包。 合并的 PrintTicket 中与用户 PrintTicket 相同的方式添加到打印筛选器管道的属性包。 该属性进行命名，如下所示：

```cpp
#define XPS_FP_JOB_LEVEL_PRINTTICKET    "JobPrintTicket"
```

期间 InitializeFilter，MTI 筛选器将添加的实现[IPrintReadStreamFactory](https://msdn.microsoft.com/library/windows/hardware/ff554338)到属性包。 此接口的一种方法**GetStream**，将一直阻止到 PrintTicket 流可用为止。 这提供了一种同步属性的访问权限。

**重要**:如果**GetStream**称为从 InitializeFilter，它将导致死锁。



## <a name="other-features"></a>其他功能


对于不支持的标准 XPS 筛选器的 PrintTicket 功能，筛选器将检查所有 PrintTicket 成员以查看是否在 GPD/PPD 中引用它们，然后指定要输出的命令。 如果是这样，将生成指定的命令。

按以下顺序映射 GPD 功能：

1. PrintSchemaKeywordMap 值指定，并且与 PrintTicket 功能名称相匹配。

2. 指定 PrintSchemaPrivateNamespaceURI 属性，而且 GPD 功能名称的 PrintTicket 功能名称匹配。 匹配功能名称并不简单，并遵循的规则数：

a. 如果**\*顺序**部分中的第一个选项是页面\_安装程序或页\_完成和 GPD 功能不会开始使用"页上"，然后尝试之前"页"预置到 GPD 功能名称匹配项。

b. 如果**\*顺序**部分中的第一个选项是文档\_安装程序或文档\_完成和 GPD 功能不会开始使用"文档"，然后"文档"预置到之前的 GPD 功能名称尝试进行匹配。

c. 如果**\*顺序**部分中的第一个选项是作业\_安装程序或作业\_完成和 GPD 功能不会开始使用"作业"，然后尝试匹配之前"作业"预置到 GPD 功能名称.

d. 不是任何字符\[A-Z\]， \[a 到 z\]， \[0-9\]或\_替换为\_然后再尝试匹配字符。 但是，如果\*NoPunctuationCharSubstitute？ 属性设置为 TRUE，则筛选器不会替换 '。 或-与\_字符。

按以下顺序映射 PPD 功能：
1. 指定 PrintSchemaKeywordMap 值并且其与 PrintTicket 功能名称匹配。

2. 指定 PrintSchemaPrivateNamespaceURI 属性，而且 PPD 功能名称的 PrintTicket 功能名称匹配。 匹配功能名称并不简单，并遵循的规则数：

a. 如果**OrderDependency**部分是 ExitServer、 序言中或 JCLSetup，并且 PPD 功能名称不以开头"作业"，则"作业"将追加到前面 PPD 功能名称然后再尝试匹配。

b. 如果**OrderDependency**部分是 DocumentSetup，并且 PPD 功能名称不以开头"文档"则"文档"然后再尝试匹配预置到 PPD 功能名称。

c. 如果**OrderDependency**部分是 AnySetup，则该筛选器执行两个匹配项检查：

i. 如果使用"文档"未开始 PPD 功能名称，然后"文档"预置到 PPD 功能名称然后再尝试匹配。

ii. 如果未找到匹配，或者如果 PPD 功能名称不以"Job"开头，然后"作业"预置到 PPD 功能名称然后再尝试匹配。

d. 如果**OrderDependency**部分是 PageSetup，并且 PPD 功能名称不以开头"页上"，则尝试匹配之前"页"预置到 PPD 功能名称。

e. 不是任何字符\[A-Z\]， \[a 到 z\]， \[0-9\]或\_替换为\_然后再尝试匹配字符。 但是，如果\*MSNoPunctuationCharSubstitute？ 字符串设置为 TRUE，该筛选器不会替换 '。 或-与\_字符。

按以下顺序映射 GPD 和 PPD 选项：
1. 指定 PrintSchemaKeywordMap 值并且其与 PrintTicket 选项名称匹配。

2. 指定 PrintSchemaPrivateNamespaceURI 属性，并且 GPD/PPD 选项名称与 PrintTicket 选项名称匹配。 匹配的选项名称并不简单，并遵循的规则数：

a. 如果 GPD/PPD 选项名称开头\[0-9\]或\_，则\_字符将追加到前面 GPD/PPD 选项名称然后再尝试匹配。 但是，下列附加规则适用：

i. 如果这是一个 GPD 选项，并\*NoPunctuationCharSubstitute？ 属性设置为 TRUE，则不会不会预置筛选器\_与\_字符。

ii. 如果这是一个 PPD 选项，并\*MSNoPunctuationCharSubstitute？ 字符串设置为 TRUE，则筛选器不会不在前面添加\_与\_字符。

b. 不是任何字符\[A-Z\]， \[a 到 z\]， \[0-9\]或\_替换为\_然后再尝试匹配字符。 但是，下列附加规则适用：

i. 如果这是一个 GPD 选项，和\*NoPunctuationCharSubstitute？ 属性设置为 TRUE，则筛选器不会替换 '。 或-与\_字符。

ii. 如果这是一个 PPD 选项，和\*MSNoPunctuationCharSubstitute？ 字符串设置为 TRUE，则筛选器不会替换 '。 或-与\_字符。

## <a name="form-to-tray-mapping"></a>送纸器映射到窗体


到 PCL6 XPS 和 XPS 到 PS 筛选器支持送纸器窗体映射表。 如果多个送纸器支持所选的媒体大小 （例如，字母），筛选器，如下所示中断关联：

1. 如果 （如 GPD 或 PPD 文件中指定） 的默认送纸器配置为使用指定的介质大小，则使用的默认送纸器。

2. 否则，该筛选器选择第一个送纸器 （上到下 GPD/PPD 文件中指定），指定的介质大小进行配置。

## <a name="extra-backside-page-suppression"></a>额外的背面页禁止显示


默认情况下，PCL6 到 XPS 和 XPS 到 PS 筛选器处理文档的情况下插入一个空白页面，包含混合媒体大小、 媒体类型、 输入或输出的箱中，双工的打印。 当筛选器插入此空页时，它将强制设备在前面的一个新的媒体上打印的下一页。 对于不需要用背面页作为输出的设备，可通过将以下关键字添加到驱动程序的 GPD 或 PPD 文件禁止此行为。

| 文件类型 | 背面页禁止显示关键字    |
|-----------|--------------------------------------|
| GPD       | \*SuppressExtraBacksidePages?:TRUE  |
| PPD       | \*MSSuppressExtraBacksidePages:True |



## <a name="optimizing-setpagedevice-commands"></a>优化 SetPageDevice 命令


使用驱动程序以及 MSxpsPS.dll PostScript 设备的默认行为是，每个页上，发出 SetPageDevice 命令，此命令声明完整的选项为页上指定集。 请注意，某些设备可能不很好地处理这种技术。

但是，如果你的设备使用 MSxpsPS.dll 和随附的 PPD 文件指定 **\*MSOptimizeSetPageDevice:True**，则以下为 PostScript 设备行为:-对于每个页面自前一页已被 SetPageDevice 命令的任何部分中的更改，其中发出新的 SetPageDevice 命令指示指定的选项集页。 但是，如果存在不以来 SetPageDevice 命令的任何部分中的任何更改前一页，然后页面不发出 SetPageDevice 命令。

## <a name="related-topics"></a>相关主题
[支持的 PrintTicket 功能](supported-printticket-features.md)  
[V4 打印机驱动程序呈现](v4-driver-rendering.md)  



