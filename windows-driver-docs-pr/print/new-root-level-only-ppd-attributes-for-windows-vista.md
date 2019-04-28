---
title: 适用于 Windows Vista 的仅限根级别的新 PPD 属性
description: 适用于 Windows Vista 的仅限根级别的新 PPD 属性
ms.assetid: 49cdfb2f-e119-4960-9e79-67e1025b753f
keywords:
- 仅限根级别属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv，仅限根级别
- PPD 属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30235aae4772d555ad99a7109b534c2f6bb67721
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330127"
---
# <a name="new-root-level-only-ppd-attributes-for-windows-vista"></a>适用于 Windows Vista 的仅限根级别的新 PPD 属性


以下列表介绍开始使用 Windows Vista 新增的 PPD 特性。 为了保持向后兼容性与早于 Windows Vista 版本的 Windows，应当在以下代码使用这些属性。

```cpp
*Ifdef: WINNT_60 ... *Endif: WINNT_60 blocks
```

### <a name="msprintschemakeywordmap"></a>MSPrintSchemaKeywordMap

**MSPrintSchemaKeywordMap**属性定义从 PPD 功能关键字映射到一个公共的打印架构功能关键字，或从 PPD PPD 选项关键字映射到公共打印架构选项关键字的打印功能架构功能。

**MSPrintSchemaKeywordMap**有两种可接受的格式：

<a href="" id="format-1"></a>格式 1  
```cpp
*MSPrintSchemaKeywordMap: PrintSchema_feature_keyword *<PPD_feature_keyword>
```

<a href="" id="format-2"></a>格式 2  
```cpp
*MSPrintSchemaKeywordMap: PrintSchema_feature_keyword PrintSchema_option_keyword *<PPD_feature_keyword> <PPD_option_keyword>
```

PPD 功能关键字前缀 (这是一个星号\[ \* \]) 在这两种格式是必需的。

有关格式 1:

-   PPD 功能关键字必须引用已在上一 PPD 文件内容中定义的 PPD 功能。

-   多个定义\* **MSPrintSchemaKeywordMap**不允许同一 PPD 功能。 如果找到多个定义，将接受仅第一个定义，并将忽略其他定义。

有关格式 2:

-   \* **MSPrintSchemaKeywordMap** PPD 功能 （通过使用格式 1） 定义必须存在任何之前\* **MSPrintSchemaKeywordMap** PPD 的定义可以显示功能的选项。

-   在中\* **MSPrintSchemaKeywordMap** PPD 选项定义，打印架构功能关键字 PPD 功能关键字的映射必须能与在以前定义的内容相同\* **MSPrintSchemaKeywordMap** PPD 功能 （通过使用格式 1） 的定义。

-   PPD 选项关键字必须引用已在上一 PPD 文件内容中定义的 PPD 功能的选项。

-   多个定义\* **MSPrintSchemaKeywordMap**不允许为同一 PPD PPD 功能的选项。 如果找到多个定义，将接受仅第一个定义，并将忽略其他定义。

如果\* **MSPrintSchemaKeywordMap**条目违反了任何上述格式规则，该条目将被忽略，并且你将获得 ppdchecker 警告的详细信息。

**重要**   \*MSPrintSchemaKeywordMap 不支持用于以下标准 PPD 功能：

\*逐份打印\*双工\*InputSlot \*OutputBin \*PageSize\*解析\*MediaType 这一点也很重要知道，如果将功能映射到已打印架构关键字使用 PPD 文件中，对应的 PrintCapabilities 文档可能还会列出该功能不止一次。 多个匹配项可能令人困惑，因此不应将功能映射到 PPD 文件中使用的打印架构关键字。

 

**请注意**  PPD 分析器自动生成 InputBin 功能 FORMSOURCE 选项，并将其映射到打印架构中的自动选择关键字。 如果 PPD 文件包含使用 InputBin 选项**MSPrintSchemaKeywordMap**属性将映射到打印架构关键字的选项，请打印架构中的功能将包含的设备命名空间中的 FORMSOURCE 选项。 自动选择将出现在 PrintCapabilities 文档和中指定的选项是指**MSPrintSchemaKeywordMap** PPD 文件的属性。

 

下面的代码示例演示的示例**MSPrintSchemaKeywordMap**部分 PPD 文件中的属性。

```cpp
*OpenUI *IHVStapling:PickOne
*DefaultIHVStapling:Disabled
*IHVStapling Enabled:"..."
*IHVStapling Disabled:"..."
*CloseUI: *IHVStapling

*MSPrintSchemaKeywordMap: Staple*IHVStapling
*MSPrintSchemaKeywordMap: StapleOn*IHVStaplingEnabled
*MSPrintSchemaKeywordMap: StapleOff*IHVStaplingDisabled
```

### <a name="msprintschemaprivatenamespaceuri"></a>MSPrintSchemaPrivateNamespaceURI

**MsPrintSchemaPrivateNamespaceURI**属性定义的专用命名空间 URI，核心驱动程序应使用它来公开私有 PPD 功能或 PrintTicket 或 PrintCapabilities 中的选项。 此 URI 将应用于任何功能或不具有显式映射的选项 (通过使用\* **MSPrintSchemaKeywordMap**定义) 到公共打印架构。

**MSPrintSchemaPrivateNamespaceURI**使用以下格式。

```cpp
*MSPPrintSchemaPrivateNamespaceURI: "<URI>"
```

&lt;URI&gt;表示 PPD QuotedValue。 根据 PPD 规范的定义，QuotedValue 允许文本 ASCII 子字符串和十六进制的子字符串。

单个打印机型号的 PPD 文件 （或文件） 应只能有一个定义的\* **MSPrintSchemaPrivateNamespaceURI** 。 如果找到多个定义，将接受仅第一个定义，并且其他人将被忽略。

下面的代码示例演示的示例**MsPrintSchemaPrivateNamespaceURI**部分 PPD 文件中的属性。

```cpp
*MSPrivateNamespaceURI:  "http://www.ihv.com/schema/2004"
```

### <a name="msisxpsdriver"></a>MSIsXPSDriver

**MSIsXPSDriver**属性使用以下格式。

```cpp
*MSIsXPSDriver:  True | False
```

您可以使用这两个 Microsoft Win32 GDI 驱动程序的 Windows Vista PScript5 驱动程序配置模块 (Ps5ui.dll) 和[新的 XPSDrv 驱动程序](xpsdrv-printer-drivers.md)。 若要使用 XPSDrv 驱动程序 PScript5 驱动程序配置模块，请在 XPSDrv 驱动程序的 PPD 数据文件必须指定**MSIsXPSDriver**并将其值设置为 True。

下面的代码示例演示分部 PPD 文件中的此属性的一个示例：

```cpp
*MSIsXPSDriver: True
```

若要使用 Win32 GDI 驱动程序 PScript5 驱动程序配置模块，你不必指定此 PPD 特性。

### <a name="msprintprocduplexoptions"></a>MSPrintProcDuplexOptions

**MSPrintProcDuplexOptions**属性使用以下格式。

```cpp
*MSPrintProcDuplexOptions:  "int"
```

此特性可具有以下值之一：

1：反向页反向双工

2：如有可能取消生成的额外的空白页

3：这两个以上

0:以上都不是

下面的代码示例演示的示例**MSPrintProcDuplexOptions**部分 PPD 文件中。

```cpp
*MSPrintProcDuplexOptions:  "2" 
```

此属性控制打印处理器中的各种进行双面打印选项。

如果**MSPrintProcDuplexOptions**为 1，它控制打印处理器是否应在反向双工反向页。

假定您已打印四页文档与每张 = 1，并且你想要使用反向打印和双面打印。 由于您想要反向打印，你想要打印的第一页之前的最后一页。 由于您希望双面打印，你想要在一张纸上打印两页。 打印处理器可以播放页中 （其中每个对数字指示将打印在纸张的一张纸的两个方面的两个页面） 以下两种格式之一：

-   格式 1:(4,3),(2,1)

-   格式 2:(3,4),(1,2)

在 Windows Vista 之前的打印处理器可能会打印格式 2 中的页面\[(3,4),(1,2)\]。 但在 Windows Vista 及更高版本，默认格式是格式 1 \[(4,3),(2,1)\]。 此更改发生，因为许多打印机有使用 2; 格式不正确的输出也就是说，打印的页未按正确的顺序排序。

如果您的打印机与格式 1 一起正常运行，不需要更改任何内容适用于 Windows Vista 及更高版本。 但是，如果在打印机使用不正确格式 1 和你想要恢复为格式 2，添加**MSPrintProcDuplexOptions**属性值为 1。

```cpp
*MSPrintProcDuplexOptions: "1"
```

对于早于 Windows Vista PScript 驱动程序，如果必须早于 Windows Vista 打印处理器，格式 2 是默认值，并不能更改的行为;否则为如果您有了 Windows Vista 打印处理器，格式 1 是默认情况下，并且不能更改的行为。

Windows Vista PScript 驱动程序。 如果必须早于 Windows Vista 打印处理器，格式 2 是默认情况下，而且 PPD 特性将被忽略;否则为如果您使用的 Windows Vista 打印处理器、 格式 1 是默认值，但可以通过更改格式**MSPrintProcDuplexOptions**属性。

如果**MSPrintProcDuplexOptions**为 2，打印处理器将取消生成的某些双工方案中的空白页。

例如，如果作业是单页作业和双工位于上 (假设每张 = 1)，仅在工作表的一端需要打印。 目前，打印机将打印一侧，然后生成在反向端空空白页。 (由于打印作业是使用双工 = 弹出工作表之前，打印机，需要两个页面。 如果第二页无法打印，某些打印机继续等待。）当前解决方案的缺点是：

-   生成的页会计软件和打印机中的页计数器中导致不准确的页计数。

-   从打印机 （在某些 Hewlett Packard DeskJet 样式打印机） 的中间页时，用户可能会尝试时打印机会尝试将它重新将其拉出。 这种情况下可能会导致硬件问题。

可以通过指定避免上述问题\* **MSPrintProcDuplexOptions**:中的"2"PPD 文件。

请注意，即使设置此属性，则空白页优化仅在以下特定情况下执行：

1.  用于反向打印，仅当整个作业可以放入纸的单面上时，才执行空白页优化 (例如，在一个一页作业使用每张 = 1 或每张多页四作业 = 4)。 如果作业需要多个表，则不会执行优化，（因为将不准确的顺序打印打印机页）。 例如，对于三页作业，页面可能会打印 3,2,1，顺序&lt;空白&gt;而不是 4,3,2，&lt;空白&gt;。

2.  空白页优化不 performedd，如果打印处理器具有用于模拟副本。 打印处理器模拟副本，如果所需的副本数不只是可以进行打印处理器的副本数。

    以下这种情况是时模拟发生并且 （如果需要），会生成空白页的示例：

    -   无法创建副本的打印机的两个副本

    在以下情况下是 examles 的时模拟不会发生，并且可以取消额外的页生成的：

    -   无法创建副本的打印机的单个副本作业
    -   五个复制作业的打印机可以使多个副本

对于早于 Windows Vista PScript 驱动程序，如果使用的是早于 Windows Vista 打印处理器，打印机将打印一个额外的空白页面上，如果认为有必要，并且不能更改的行为;否则为如果您使用的 Windows Vista 打印处理器，打印机将打印一个额外的空白页面上，如果认为有必要，并且不能更改的行为。

Windows Vista PScript 驱动程序。 如果必须早于 Windows Vista 打印处理器，打印机将打印一个额外的空白页面上，如果认为有必要，并且将忽略 PPD 属性;否则为如果您使用的 Windows Vista 的打印处理器，并且相应的 PPD 特性和正确的条件是否存在 （即，有关防止前面所述的条件保留为空页打印），打印机将不打印空白页。

### <a name="msbidiqueryfile"></a>MSBidiQueryFile

**MSBiDiQueryFile**属性使用以下格式。

```cpp
*MSBidiQueryFile: "filename"
```

使用**MSBiDiQueryFile**若要指定包含打印机驱动程序的自动配置 BidiQuery 和 BidiResponse 数据 GPD 或 GDL 文件名称。 GPD 或 GDL 文件名称不应指定任何路径。

下面的代码示例演示的示例**MSBiDiQueryFile**部分 PPD 文件中。

```cpp
*MSBidiQueryFile: "ACnfgPS.GDL"
```

### <a name="msxpsmaxcopies"></a>MSXPSMaxCopies

**MSXPSMaxCopies**属性使用以下格式。

```cpp
*MSXPSMaxCopies: "int"
```

使用**MSXPSMaxCopies**以指定的最大的 XPSDrv 打印机驱动程序支持的副本。

下面的代码示例演示的示例**MSXPSMaxCopies**部分 PPD 文件中。

```cpp
*MSXPSMaxCopies: "99"
```

 

 




