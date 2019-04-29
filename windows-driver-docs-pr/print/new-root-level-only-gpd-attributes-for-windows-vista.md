---
title: 适用于 Windows Vista 的仅限根级别的新 GPD 属性
description: 适用于 Windows Vista 的仅限根级别的新 GPD 属性
ms.assetid: 09f38459-6062-4d2a-9aee-929aa60193cf
keywords:
- 仅限根级别属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv，仅限根级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 396b844eecb6d4747d200856fa63ee0833bdac73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355899"
---
# <a name="new-root-level-only-gpd-attributes-for-windows-vista"></a>适用于 Windows Vista 的仅限根级别的新 GPD 属性


以下列表介绍开始使用 Windows Vista 新增的 GPD 特性。 为了保持向后兼容性与早于 Windows Vista 版本的 Windows，应当在以下代码使用这些属性。

```cpp
*Ifdef: WINNT_60 ... *Endif: WINNT_60 blocks
```

### <a name="printprocduplexoptions"></a>PrintProcDuplexOptions

**PrintProcDuplexOptions**属性可以控制打印处理器中的各种进行双面打印选项。 此特性可具有以下值之一：

1：反向页反向双工

2：如有可能取消生成的额外的空白页

3：这两个以上

0:以上都不是

如果**PrintProcDuplexOptions**为 1，它控制打印处理器是否应在反向双工反向页。

假定您已打印四页文档与每张 = 1，并且你想要使用反向打印和双面打印。 由于您想要反向打印，你想要打印的第一页之前的最后一页。 由于您希望双面打印，你想要在一张纸上打印两页。 打印处理器可以播放页中 （其中每个对数字指示将打印在纸张的一张纸的两个方面的两个页面） 以下两种格式之一：

-   格式 1:(4,3),(2,1)

-   格式 2:(3,4),(1,2)

在 Windows Vista 之前的打印处理器可能会打印格式 2 中的顺序\[(3,4),(1,2)\]。 但在 Windows Vista 及更高版本，默认格式是格式 1 \[(4,3),(2,1)\]。 此更改发生，因为许多打印机有使用 2; 格式不正确的输出也就是说，打印的页未按正确的顺序排序。

但如果您的打印机与格式 1 一起正常运行，您不需要更改任何内容适用于 Windows Vista 及更高版本。 但是，如果您的打印机未正确使用格式 1 并想要恢复为格式 2，添加下面的代码示例 GPD 文件。

```cpp
*Ifdef: WINNT_60
*PrintProcDuplexOptions: 1
*Endif: WINNT_60
```

格式 1 可能在某些方向中更好地运行，或输入和输出纸和格式 2 的某些组合可能在其他组合中更好地运行。 因此，您可以将放**PrintProcDuplexOptions**开关/用例构造中的属性。

早于 Windows Vista Unidrv 驱动程序，如果您有了早于 Windows Vista 打印处理器，格式 2 是默认值，并不能更改格式;否则为如果您有了 Windows Vista 打印处理器，格式 1 是默认值，并且不能更改的格式。

对于 Windows Vista Unidrv 驱动程序，如果您有了早于 Windows Vista 打印处理器，格式 2 是默认情况下，和 GPD 特性将被忽略;否则为如果您使用的 Windows Vista 打印处理器、 格式 1 是默认值，但可以通过更改格式**PrintProcDuplexOptions**属性。

如果**PrintProcDuplexOptions**为 2，它会阻止生成的某些双工方案中的空白页。

此属性控制是否应向发送额外的空白页打印机执行双面打印时。 例如，如果作业是一个页作业和双工模式是在 (假设每张 = 1)，仅在工作表的一端需要打印。 目前，打印机将打印一侧，然后生成在反向端空空白页。 (由于打印作业是使用双工 = 弹出工作表之前，打印机，需要两个页面。 如果第二页无法打印，某些打印机继续等待。）当前解决方案的缺点是：

-   生成的页会计软件和打印机中的页计数器中导致不准确的页计数。

-   从打印机 （在某些 Hewlett Packard DeskJet 样式打印机） 的中间页时，用户可能会尝试时打印机会尝试将它重新将其拉出。 这种情况下可能会导致硬件问题。

可以通过指定避免上述问题\* **PrintProcDuplexOptions**:2 GPD 文件中。

请注意，即使设置此属性，则空白页优化仅在以下特定情况下执行：

1.  用于反向打印，仅当整个作业可以放入纸的单面上时，才执行空白页优化 (例如，具有 n 个向上的一页作业 = 1 或每张多页四作业 = 4)。 如果作业需要多个表，则不会执行优化，（因为将不准确的顺序打印打印机页）。 例如，对于三页作业，页面可能会打印 3,2,1，顺序&lt;空白&gt;而不是 4,3,2，&lt;空白&gt;。

2.  如果打印处理器具有用于模拟副本，则不执行空白页优化。 打印处理器模拟副本，如果所需的副本数不只是可以进行打印处理器的副本数。

    以下这种情况是时模拟发生并且 （如果需要），会生成空白页的示例：

    -   无法创建副本的打印机的两个副本

    在以下情况下是 examles 的时模拟不会发生，并且可以取消额外的页生成的：

    -   无法创建副本的打印机的单个副本作业
    -   可以使多个复制的打印机的五个复制作业

**Usage of PrintProcDuplexOptions**

```cpp
*Ifdef: WINNT_60
*PrintProcDuplexOptions: 2
*Endif: WINNT_60 
```

在某些情况下，可能不介意额外的页打印时在其他情况下，执行。 因此，可以放置**PrintProcDuplexOptions**开关/用例构造中的属性。

早于 Windows Vista Unidrv 驱动程序，如果使用的是早于 Windows Vista 打印处理器，打印机将打印一个额外的空白页面上，如果认为有必要，并且不能更改此行为;否则为如果您使用的 Windows Vista 打印处理器，打印机将打印一个额外的空白页面上，如果认为有必要，并且不能更改此行为。

对于 Windows Vista Unidrv 驱动程序，如果使用的是早于 Windows Vista 打印处理器、 打印机将打印一个额外的空白页面上，如果认为有必要，和 GPD 特性将被忽略;否则为如果您使用的 Windows Vista 的打印处理器，并相应 GPD 属性和正确的条件是否存在 （即，有关防止前面所述的条件保留为空页打印），打印机将不打印空白页。

### <a name="preanalysisoptions"></a>PreAnalysisOptions

**PreAnalysisOptions**属性可以具有以下值之一：

0:禁用所有预分析模式。

1：默认模式。 启用单色的 z 顺序的文本分析和空白外优化。 有关使用可下载的字体或设备字体支持和高分辨率设备启用此模式 (600 dpi 或更高版本)、 24 bpp 呈现模式。

2：启用 1 bpp 优化 24 bpp ImageProcessing 回调函数。

4:启用设备 StretchBlt 支持。

8:启用供应商预分析模式。

16:启用 1 bpp 其中带区之前转换为 24 bpp 调用 ImageProcessing 回调函数的调试模式。

### <a name="usebmpfontcompression"></a>UseBMPFontCompression?

**UseBMPFontCompression？** 属性控制是否 Unidrv 字体下载为位图时应压缩的数据。 默认值**UseBMPFontCompression？** 是**FALSE**，这意味着如果此属性不存在 GPD 文件中，Unidrv 不会执行压缩。 此默认值维护与较旧版本的 Unidrv 不具有的位图字体压缩功能的兼容性。 应将此属性设置为 **，则返回 TRUE**仅当您的打印机支持的位图字体 compressionThe 压缩位图字符数据是以运行长度与行重复的压缩格式。

### <a name="usemode5compression"></a>UseMode5Compression？

**UseMode5Compression？** 属性控制是否 UniDrv 应使用模式 5 压缩。 模式 5 （或方法 5） 压缩是允许多个其他压缩方法 （如 Unencoded、 TIFF 或增量行） 组合的使用的自适应压缩。 默认值**UseMode5Compression？** 是**FALSE**，这意味着 Unidrv 将不会执行自适应压缩，如果此属性不存在 GPD 中。 此默认值维护与较旧版本的 Unidrv 不具有自适应的压缩功能的兼容性。 应将此属性设置为 **，则返回 TRUE**仅当您的打印机支持自适应压缩。

### <a name="usehpglpolylineencoding"></a>UseHPGLPolylineEncoding?

**UseHPGLPolylineEncoding？** 属性控制是否 Unidrv 应使用 polyline 编码。 HP/2 最多可支持笔 / 向下笔/绘制向量绘制相对绝对/绘图命令。 折线编码 (PE) 命令是表示矢量的更高效的方法。

默认值为**UseHPGLPolylineEncoding？** 是**FALSE**，这意味着如果此属性中不存在 GPD，Unidrv 不会使用 PE 命令。 此默认值维护与较旧版本的 Unidrv 不具有对 PE 命令支持的兼容性。 您应将该值设置 **，则返回 TRUE**仅当您的打印机支持编码的折线。

### <a name="printschemaprivatenamespaceuri"></a>PrintSchemaPrivateNamespaceURI

**PrintSchemaPrivateNamespaceURI**属性定义的专用命名空间 URI，核心驱动程序应使用它来公开私有 PPD 功能或 PrintTicket 或 PrintCapabilities 中的选项。 该属性必须出现在 GPD 文档的根，并且包含将用于在 Printticket 和 PrintCapabilities 文档中定义一个命名空间 URI 的 ASCII 表示形式。 URI，反过来，将与相关联的所有功能和不具有显式映射到公共架构，或核心驱动程序不能识别的选项。

### <a name="printschemakeywordmap"></a>PrintSchemaKeywordMap

**PrintSchemaKeywordMap**属性将会显示在功能和选项下，构造 GPD 文件中。 此属性指示应使用的打印机定义功能什么公共打印架构名称。 您可以重命名在 GPD 文件中，除双工和逐份打印，使用 PrintTicket 中的指定任何选项**PrintSchemaKeywordMap**属性。

**请注意**   GPD 分析器将忽略此属性显式识别，包括页面大小和颜色的功能。

 

所有值应都括在引号中。 如果有使用 GPD 中指定的代码页，将为 Unicode 转换它们。 作为其他 GPD 属性相同的方式解决的任何特性的重复的定义：读取的最后一个定义优先。

**重要**  相应 PrintCapabilities 文档如果向已在使用 GPD 文件中的打印架构关键字映射一项功能，可能会超过一次列出该功能。 多个匹配项可能令人困惑，因此不应将功能映射到 GPD 文件中使用的打印架构关键字。

 

**请注意**  GPD 分析器自动生成 InputBin 功能 FORMSOURCE 选项，并将其映射到打印架构中的自动选择关键字。 如果 GPD 文件包含使用 InputBin 选项**PrintSchemaKeywordMap**属性将映射到打印架构关键字的选项，请打印架构中的功能将包含的设备命名空间中的 FORMSOURCE 选项。 自动选择将出现在 PrintCapabilities 文档和中指定的选项是指**PrintSchemaKeywordMap** GPD 文件的属性。

 

下面的代码示例显示了完整的 GPD 文件以显示布局。

```cpp
*Feature: HPSTAPLER
{
    *Name: "Staple"
    *DefaultOption: Off
    * PrintSchemaKeywordMap: "Staple"

    *Option: Off
    {
        *Name: "Off"
        * PrintSchemaKeywordMap: "Off"
    }
 
    *Option: On
    {
        *Name: "On"
        * PrintSchemaKeywordMap: "On"
    }
}
```

### <a name="isxpsdriver"></a>IsXPSDriver

**IsXPSDriver**属性使用以下 GPD 语法。

```cpp
*IsXPSDriver?: TRUE | FALSE
```

您可以使用 Windows Vista Unidrv 配置模块 (Unidrvui.dll) Microsoft Win32 GDI 驱动程序和新[XPSDrv 驱动程序](xpsdrv-printer-drivers.md)。 若要使用 XPSDrv 驱动程序 Unidrv 配置模块，请在 XPSDrv 驱动程序的 gpd 分析数据文件必须指定**IsXPSDriver**属性，并将其值设置为**TRUE**。

例如，如果您有的 XPS 驱动程序，使用下面的代码。

```cpp
*IsXPSDriver?: TRUE
```

若要使用 Win32 GDI 驱动程序 Unidrv 配置模块，你不必指定此属性。

### <a name="useimageforhatchbrush"></a>UseImageForHatchBrush?

**UseImageForHatchBrush？** 属性使用以下 GPD 语法。

```cpp
*Ifdef: WINNT_60
*UseImageForHatchBrush?: TRUE
*Endif: WINNT_60 
```

在 Microsoft Windows Server 2003 或 Windows XP 中，当 Unidrv 打印在 HP/2 模式下，如果在收到阴影画笔[ **DrvRealizeBrush** ](https://msdn.microsoft.com/library/windows/hardware/ff556273)函数，以便打印机选择 Unidrv 发送命令相应的阴影画笔。 Unidrv 不控制阴影画笔的呈现方式。 例如，通过解析通常控制线之间的间距。 在更高的分辨率，间距获取小，同时在较低的分辨率，间距为更高版本。 因此，文档可能以不同方式打印如果使用不同的解决方法。

在 Windows Vista 中，如果指定了 GPD **UseImageForHatchBrush？** 特性 Unidrv 呈现一个位图表面上的阴影画笔，然后将该位图发送到设备。 Unidrv，因此，有一些控件上的阴影画笔的呈现方式。

### <a name="reversebandorder"></a>ReverseBandOrder?

**ReverseBandOrder？** 属性使用以下 GPD 语法。

```cpp
*Ifdef: WINNT_60
*ReverseBandOrder?: TRUE
*Endif: WINNT_60 
```

值**ReverseBandOrder？** 是**TRUE**或**FALSE**指示是否启用反向条带。 此属性会导致条带将按相反的顺序执行。 例如，对于纵向页上，条带会发生从底部到顶部而不是从上到下。

此属性实质上是相同 ReverseBandOrderForEvenPages？，只不过**ReverseBandOrder？** 甚至被视为如果双工不处于活动状态 (**ReverseBandOrderForEvenPages？** works 仅当双工为 ON），并且它适用于所有页 (**ReverseBandOrderForEvenPages？** 仅适用于偶数页)。 有关如何使用的详细信息**ReverseBandOrder？** 和其他相关的信息，请参阅\* **ReverseBandOrderForEvenPages？**。 尤其注意插件必须撤消扫描行和扫描行中的位。

可以使用的组合\*ReverseBandOrderForEvenPages？ 和\* **ReverseBandOrder？**。

当仅**ReverseBandOrder？** 设置为**TRUE**，条带将反转的所有页面。

当仅**ReverseBandOrderForEvenPages？** 设置为**TRUE**，条带将反转为甚至 pagesonly 如果打印机正在打印，双工。 如果未设置双工， **ReverseBandOrderForEvenPages？** 设置将被忽略。

当同时**ReverseBandOrder？** 并**ReverseBandOrderForEvenPages？** 设置，将发生以下情况：

-   如果双工为 ON，将反向条带执行奇数页 （即 1、 3、 5、 7 和等等）。

-   如果双工为 OFF，则反向法执行的所有页面。

### <a name="bidiqueryfile"></a>BidiQueryFile

**BidiQueryFile**属性使用以下 GPD 语法。

```cpp
*BidiQueryFile: <GPD or GDL file name>
```

使用**BidiQueryFile**若要指定 GPD 或 GDL 文件名称，其中包含打印机驱动程序的自动配置**BidiQuery**或**BidiResponse**数据。 GPD 或 GDL 文件名称不应指定任何路径。 如果自动配置数据包含在驱动程序的数据文件 GPD 文件，还可以作为的值指定该 GPD 文件**BidiQueryFile**属性。

下面的代码示例演示分部 GPD 文件中此属性的一个示例。

```cpp
*Ifdef: WINNT_60
*BidiQueryFile: "ACnfgUni.GDL"
*Endif: WINNT_60
```

 

 




