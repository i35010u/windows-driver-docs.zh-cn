---
title: 标准 XPS 筛选器
description: Windows 提供了两个 (标准) XPS 筛选器，用于支持从 XPS 到 PCL6 和 PostScript level 3 的内置转换。
ms.assetid: 6404D215-8154-4604-A67B-19B20D1CF229
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a166cdbe34bb37e2bd0a870a541c398ce02ac63
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212659"
---
# <a name="standard-xps-filters"></a>标准 XPS 筛选器


Windows 提供了两个 (标准) XPS 筛选器，用于支持从 XPS 到 PCL6 和 PostScript level 3 的内置转换。

Windows 提供的筛选器可用于打印类驱动程序和特定于模型的 v4 打印驱动程序。 这些 XPS 筛选器可与 IHV 功能筛选器和 IHV 后处理筛选器结合，以确保与现有固件实现兼容。

**注意**  这些 Windows 提供的 XPS 筛选器不能重新分发，并且不适用于 v3 打印驱动程序。



## <a name="the-manifest-file"></a>清单文件


若要使用 Windows 提供的 XPS 筛选器，v4 驱动程序清单文件必须使用 **DriverConfig** 部分下的 RequiredFiles 指令来指定筛选器。 下面是筛选器的名称：

*MSxpsPCL6.dll*。 提供从 XPS 到 PCL6 的转换。
*MSxpsPS.dll*。 提供从 XPS 到 PostScript level 3 的转换。
使用其中一个筛选器不需要任何 INF 更新，并且不支持再分发。
## <a name="print-filter-pipeline-configuration"></a>打印筛选器管道配置


若要将打印筛选器管道配置为使用这些筛选器，必须创建配置文件，如以下示例中所示。

指定转换为 PCL6 的示例配置文件。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Filters>
  <Filter dll="MSxpsPCL6.dll" clsid="{3821E518-33AF-4d17-92B3-28EB410D46B6}" name="Microsoft XPS to PCL6">
    <Input guid="{4d47a67c-66cc-4430-850e-daf466fe5bc4}" comment="IID_IPrintReadStream" />
    <Output guid="{65bb7f1b-371e-4571-8ac7-912f510c1a38}" comment="IID_IPrintWriteStream" />
  </Filter>  
</Filters>
```

指定转换到 PostScript 的示例配置文件。

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


标准 XPS 筛选器支持许多常见功能。 所有功能定义使用驱动程序的 GPD 或 PPD 文件。 *MSxpsPCL6.dll*筛选器需要使用 GPD 文件进行配置，并且*MSxpsPS.dll*筛选器需要使用 PPD 文件进行配置。 除非另有说明，否则，如果为功能指定了自定义 PDL 命令，则将使用该命令。

如果在任何特定的节下存在注入字符串 (使用** \* Order**命令) 指定，则在 GPD 文件的情况下，筛选器将对这些字符串的内容进行一些假设，并避免发送默认命令。 这是因为在这种情况下，发送默认命令可能会导致命令冲突。 因此，GPD 文件的创建者必须遵循以下准则：

-   作业 \_ 设置。 \# o PCL6 Binary Stream 标头 (例如： ") &lt; SP &gt; HP-PCL XL; 1; &lt;CR &gt; &lt; LF &gt; ") 必须存在。
    o BeginSession 运算符必须存在，包括所有必需的属性。
    o OpenDataSource 运算符必须存在，包括所有必需的属性。
-   页面 \_ 设置。 \# o BeginPage 运算符必须存在，包括所有必需的属性。
-   页面 \_ 完成。 \# o EndPage 运算符必须存在。
-   作业 \_ 完成。 \# o CloseDataSource 运算符必须存在。
    o EndSession 运算符必须存在。
    o EndPJLCommands 运算符必须存在。

XPS 标准筛选器生成相应的 PDL 数据，以根据 \* PrintableArea、 \* PrintableOrigin 或 ImageableArea 命令设置页面的来源 \* 。 为了避免与预期来源的额外偏移，GPD 文件不应在 \* 其纸张大小的 Cmd 字符串定义中指定任何 = SetPageOrigin 命令。

有关标准 XPS 筛选器支持的 PrintTicket 功能的详细信息，请参阅 [支持的 Printticket 功能](supported-printticket-features.md)。

## <a name="retrieving-printticket-in-post-processing-filters"></a>正在处理后处理筛选器中的 PrintTicket


在随 Windows 8 一起发布的 v4 驱动程序模型中，当你在其中一个 MSxps 筛选器后添加后处理筛选器时，有时你还必须添加预处理筛选器。 需要添加预处理筛选器才能捕获作业级打印票证。 但这种方法实质上是在基于流的 MSxps 筛选器之前添加基于对象模型的筛选器，导致反序列化，然后对打印数据进行序列化以只提取 PrintTicket。

在 Windows 8.1 中，用户默认值 PrintTicket 与 MSxps 筛选器中的作业级 PrintTicket 合并，并将合并的 PrintTicket 添加到打印筛选器管道的属性包。 合并的 PrintTicket 按照与用户 PrintTicket 相同的方式添加到打印筛选器管道的属性包中。 属性的命名方式如下：

```cpp
#define XPS_FP_JOB_LEVEL_PRINTTICKET    "JobPrintTicket"
```

在 InitializeFilter 期间，MTI 筛选器会将 [IPrintReadStreamFactory](/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory) 的实现添加到属性包中。 此接口的一种方法 **system.resources.resourcemanager.getstream**会一直阻止，直到 PrintTicket 流可用。 这提供了一种方法来同步对属性的访问。

**重要提示**  ：如果从 InitializeFilter 调用 **system.resources.resourcemanager.getstream** ，则会导致死锁。



## <a name="other-features"></a>其他功能


对于标准 XPS 筛选器不支持的 PrintTicket 功能，筛选器将检查所有 PrintTicket 成员，以查看它们是否在 GPD/PPD 中引用，然后指定要输出的命令。 如果是这样，则将生成指定的命令。

GPD 功能按以下顺序映射：

1. 指定了 PrintSchemaKeywordMap 值并与 PrintTicket 功能名称匹配。

2. 指定了 PrintSchemaPrivateNamespaceURI 特性，并且 GPD 功能名称与 PrintTicket 功能名称匹配。 匹配功能名称并不是很简单，并遵循若干规则：

a. 如果第一个选项的 " ** \* 顺序**" 部分为 \_ "页面设置" 或 \_ "页面完成"，并且 "GPD" 功能不以 "page" 开头，则在尝试匹配之前，将 "page" 预置到 GPD 功能名称之前。

b. 如果第一个选项的 " ** \* 顺序**" 部分为 \_ "doc 安装" 或 \_ "doc 完成"，并且 "GPD" 功能不以 "document" 开头，则在尝试匹配之前，"文档" 会预置到 GPD 功能名称之前。

c. 如果第一个选项的 " ** \* 顺序**" 部分为 \_ "作业设置" 或 \_ "作业完成"，并且 "GPD" 功能不以 "job" 开头，则在尝试匹配之前，"作业" 会预置到 GPD 功能名称之前。

d. 在 \[ \] 尝试匹配之前，不为 a-z、a-z \[ \] 、 \[ 0-9 或 "" 的任何字符 \] \_ 都将替换为 " \_ " 字符。 但是，如果 " \* NoPunctuationCharSubstitute" 属性设置为 "TRUE"，则筛选器不会替换 "." 或 "-" \_ 字符。

PPD 功能按以下顺序映射：
1. 指定了 PrintSchemaKeywordMap 值，并且它与 PrintTicket 功能名称匹配。

2. 指定了 PrintSchemaPrivateNamespaceURI 属性，并且 PPD 功能名称与 PrintTicket 功能名称匹配。 匹配功能名称并不是很简单，并遵循若干规则：

a. 如果 **OrderDependency** 部分为 ExitServer、Prolog 或 JCLSetup，并且 ppd 功能名称不以 "Job" 开头，则在尝试匹配之前，"作业" 将会预置到 PPD 功能名称之前。

b. 如果 **OrderDependency** 部分为 DocumentSetup，并且 ppd 功能名称未以 "Document" 开头，则在尝试匹配之前，将 "document" 预置到 PPD 功能名称之前。

c. 如果 **OrderDependency** 部分为 AnySetup，则筛选器将执行两个匹配检查：

i. 如果 PPD 功能名称不以 "Document" 开头，则在尝试匹配之前，"文档" 会预置到 PPD 功能名称上。

ii. 如果找不到匹配项，或者 PPD 功能名称不是以 "Job" 开头，则在尝试匹配之前，"作业" 将附加到 PPD 功能名称之前。

d. 如果 **OrderDependency** 部分为 PageSetup，并且 ppd 功能名称不以 "Page" 开头，则在尝试匹配之前，将在 ppd 功能名称前附加 "page"。

e. 在 \[ \] 尝试匹配之前，不为 a-z、a-z \[ \] 、 \[ 0-9 或 "" 的任何字符 \] \_ 都将替换为 " \_ " 字符。 但是，如果 \* MSNoPunctuationCharSubstitute？ String 设置为 TRUE，则筛选器不会替换 "." 或 "-" \_ 字符。

GPD 和 PPD 选项按以下顺序映射：
1. 指定了 PrintSchemaKeywordMap 值，并且它与 PrintTicket 选项名称匹配。

2. 指定了 PrintSchemaPrivateNamespaceURI 属性，并且 GPD/PPD 选项名称与 PrintTicket 选项名称匹配。 匹配选项名称并不简单，并且遵循了若干规则：

a. 如果 GPD/PPD 选项名称开头为 \[ 0-9 \] 或 " \_ "，则在 \_ 尝试匹配之前，"" 字符会附加到 GPD/PPD 选项名称之前。 但是，以下附加规则适用：

i. 如果这是 GPD 选项，并且 \* NoPunctuationCharSubstitute？特性设置为 TRUE，则筛选器不在 "" 前面追加 "" \_ \_ 字符。

ii. 如果这是一个 PPD 选项，并且 \* MSNoPunctuationCharSubstitute？字符串设置为 TRUE，则筛选器不在 "" 前面追加 "" \_ \_ 字符。

b. 在 \[ \] 尝试匹配之前，不为 a-z、a-z \[ \] 、 \[ 0-9 或 "" 的任何字符 \] \_ 都将替换为 " \_ " 字符。 但是，以下附加规则适用：

i. 如果这是 GPD 选项，并且 \* NoPunctuationCharSubstitute？特性设置为 TRUE，则筛选器不会替换 "." 或 "-" \_ 字符。

ii. 如果这是一个 PPD 选项，并且 \* MSNoPunctuationCharSubstitute？字符串设置为 TRUE，则筛选器不会替换 "." 或 "-" \_ 字符。

## <a name="form-to-tray-mapping"></a>窗体到托盘的映射


XPS 到 PCL6 和 XPS 到 PS 的筛选器支持窗体到托盘的映射表。 如果多个送纸器支持所选媒体大小 (例如，字母) ，则筛选器将按如下方式打破关联：

1. 如果在 GPD 或 PPD 文件中指定的默认任务栏 () 配置为使用指定的媒体大小，则使用默认纸盒。

2. 否则，筛选器将选择第一个送纸器 (上到下，因为在配置有指定介质大小的 GPD/PPD 文件) 中指定了第一个托盘。

## <a name="extra-backside-page-suppression"></a>额外的背面页面抑制


默认情况下，通过插入空页面，XPS 到 PCL6 和 XPS 到 PS 的筛选器可以处理包含混合介质大小、介质类型、输入或输出箱的文档的双工打印。 当筛选器插入此空页面时，它会强制设备打印新介质的前一页。 对于不需要输出背面页面的设备，可以通过将以下关键字添加到驱动程序的 GPD 或 PPD 文件来禁止显示此行为。

| 文件类型 | 背面页面抑制关键字    |
|-----------|--------------------------------------|
| GPD       | \*SuppressExtraBacksidePages？： TRUE  |
| 信息库       | \*MSSuppressExtraBacksidePages： True |



## <a name="optimizing-setpagedevice-commands"></a>优化 SetPageDevice 命令


使用驱动程序与 MSxpsPS.dll 的 PostScript 设备的默认行为是：为每个页面发出 SetPageDevice 命令，此命令声明为页面指定的一组完整的选项。 请注意，某些设备在此方法中可能无法正常运行。

但是，如果设备使用 MSxpsPS.dll，而附带的 PPD 文件指定** \* MSOptimizeSetPageDevice： True**，则以下是 PostScript 设备行为：-对于自上一页面后 SetPageDevice 命令的任何部分发生了更改的每个页面，将发出新的 SetPageDevice 命令，以指示为页面指定的选项集。 但是，如果自上一页面起，SetPageDevice 命令的任何部分没有任何更改，则不会为该页发出 SetPageDevice 命令。

## <a name="related-topics"></a>相关主题
[支持的 PrintTicket 功能](supported-printticket-features.md)  
[V4 打印机驱动程序渲染](v4-driver-rendering.md)