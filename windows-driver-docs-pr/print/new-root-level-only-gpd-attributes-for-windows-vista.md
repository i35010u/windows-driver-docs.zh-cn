---
title: 适用于 Windows Vista 的仅限根级别的新 GPD 属性
description: 适用于 Windows Vista 的仅限根级别的新 GPD 属性
ms.assetid: 09f38459-6062-4d2a-9aee-929aa60193cf
keywords:
- 仅限根级别的属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv，仅限根级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a706e39a1f776c9232eb7c0f85d5c4ed0d14b701
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209531"
---
# <a name="new-root-level-only-gpd-attributes-for-windows-vista"></a>适用于 Windows Vista 的仅限根级别的新 GPD 属性


以下列表描述了从 Windows Vista 开始的新的 GPD 属性。 若要保持与 Windows Vista 以前版本的向后兼容性，应将这些属性包含在以下代码中。

```cpp
*Ifdef: WINNT_60 ... *Endif: WINNT_60 blocks
```

### <a name="printprocduplexoptions"></a>PrintProcDuplexOptions

**PrintProcDuplexOptions**属性控制打印处理器中的各种双工选项。 此属性可以具有以下值之一：

1：反向双工页

2：如果可能，禁止生成额外的空白页

3：上述两个

0：以上均不是

如果 **PrintProcDuplexOptions** 为1，则它控制打印处理器是否应反转双工上的页面。

假设您必须打印一个包含 n-up = 1 的四页文档，并且您想要使用反转打印和双工打印。 由于需要进行反向打印，因此需要在第一页之前打印最后一页。 由于需要双面打印，因此需要在一张纸上打印两页。 打印处理器可以使用以下两种格式中的一种来播放页 (其中，每对数字表示将在单张纸的两面上打印的两页) ：

-   格式1： (4，3) ， (2，1) 

-   格式2： (3，4) ， (1，2) 

在 Windows Vista 之前，打印处理器会按 "格式 2 \[ (3，4) ， (1，2) 来打印订单 \] 。 但在 Windows Vista 和更高版本中，默认格式为 format 1 \[ (4，3) ， (2，1) \] 。 发生此更改的原因是许多打印机的输出格式不正确，格式为 2;也就是说，打印的页面未按正确顺序排列。

但是，如果您的打印机在格式为1的情况下正常工作，则不需要为 Windows Vista 和更高版本更改任何内容。 但是，如果您的打印机的格式不正确，并且您想要恢复为格式2，请将下面的代码示例添加到您的 GPD 文件中。

```cpp
*Ifdef: WINNT_60
*PrintProcDuplexOptions: 1
*Endif: WINNT_60
```

格式1在某些方向或输入和输出送纸器组合时可能更好，格式2在其他组合中可能更好。 因此，可以将 **PrintProcDuplexOptions** 属性放入交换机/case 构造。

对于 Windows Vista 之前的 Unidrv 驱动程序，如果您具有 Windows Vista 以前的打印处理器，则默认情况下，"格式 2" 为默认值，不能更改格式;否则，如果你有 Windows Vista 打印处理器，则默认情况下将使用格式1，并且无法更改格式。

对于 Windows Vista Unidrv 驱动程序，如果使用的是 Windows Vista 以前的打印处理器，则默认值为 "格式 2"，将忽略 "GPD" 属性;否则，如果你有 Windows Vista 打印处理器，则默认情况下使用格式1，但你可以使用 **PrintProcDuplexOptions** 属性更改格式。

如果 **PrintProcDuplexOptions** 为2，则会阻止在某些双工方案中生成空白页。

此属性控制在执行双工打印时是否应向打印机发送额外的空白页。 例如，如果作业为单页作业，并且双工处于开启状态 (假设 n 向上 = 1) ，则只需打印工作表的一侧。 目前，打印机将打印一侧，然后在反面生成空的空白页。  (因为打印作业是以双工 = on 启动的，所以打印机在弹出工作表之前需要两个页面。 如果第二页未打印，则某些打印机会继续等待。 ) 当前解决方案的缺点：

-   生成的页面导致记帐软件中的页计数不正确，并在打印机中出现页计数器。

-   如果页面上的 Hewlett Packard DeskJet) 打印机中的页面的 (一半，则用户可能会尝试将其拉出，同时打印机会尝试将其取回。 这种情况可能导致硬件问题。

可以通过 \* 在 GPD 文件中指定**PrintProcDuplexOptions**：2来避免上述问题。

请注意，即使设置了此属性，仅在以下有限情况下才会执行空白页面优化：

1.  对于反向打印，仅当整个作业可以放在纸张单面上时，才会执行空白页优化 (例如，一页作业，其中包含 n 个（n） = 1 或四页作业，其中包含 n 个) 。 如果作业需要多个工作表，则不会执行优化 (因为打印机页将按不准确的顺序打印) 。 例如，对于三页作业，可以按订单3、2、1、 &lt; 空白 &gt; 而不是4，3，2，将页面打印为 &lt; 空白 &gt; 。

2.  如果打印处理器必须模拟副本，则不执行空白页优化。 如果所需的副本数大于打印处理器可以制作的副本数，打印处理器会模拟副本。

    以下情况是发生模拟的一个示例，并 (如有必要) 生成空白页：

    -   不能制作副本的打印机的两个副本

    以下情况 examles 不发生模拟时的情况，您可以取消额外的页面生成：

    -   不能制作副本的打印机的单个复制作业
    -   5-复制作业，适用于可生成多个 copys 的打印机

**PrintProcDuplexOptions 的用法**

```cpp
*Ifdef: WINNT_60
*PrintProcDuplexOptions: 2
*Endif: WINNT_60 
```

在某些情况下，在其他情况下，您可能不介意进行额外的页面打印。 因此，可以将 **PrintProcDuplexOptions** 属性放入交换机/case 构造。

对于 Windows Vista 以前的 Unidrv 驱动程序，如果有 Windows Vista 以前的打印处理器，打印机将打印一个额外的空白页面（如果有必要），并且无法更改此行为;否则，如果有 Windows Vista 打印处理器，打印机将打印额外的空白页面（如果有必要），并且无法更改此行为。

对于 Windows Vista Unidrv 驱动程序，如果你具有 Windows Vista 以前的打印处理器，则打印机将打印一个额外的空白页面（如果有必要），并且将忽略 GPD 属性;否则，如果你有 Windows Vista 打印处理器，并且存在适当的 GPD 属性和适当的条件 (即，先前介绍的用于防止空白页面打印) 的情况下，打印机将不会打印空白页面。

### <a name="preanalysisoptions"></a>PreAnalysisOptions

**PreAnalysisOptions**属性可以具有以下值之一：

0：禁用所有预分析模式。

1：默认模式。 启用 "单色 z 顺序文本分析" 和 "空白带优化"。 对于具有可下载字体或设备字体支持的设备，以及高分辨率 (600 dpi 或更高分辨率) 24 bpp 渲染模式，会启用此模式。

2：为 24 bpp ImageProcessing 回调函数启用 1 bpp 优化。

4：启用设备 StretchBlt 支持。

8：启用供应商预分析模式。

16：在调用 ImageProcessing 回调函数之前，启用 1 bpp 的调试模式，其中带区转换为 24 bpp。

### <a name="usebmpfontcompression"></a>UseBMPFontCompression?

**UseBMPFontCompression？** 属性控制在将字体作为位图下载时，Unidrv 是否应压缩数据。 **UseBMPFontCompression？** 的默认值为**FALSE**，这意味着如果 GPD 文件中不存在此属性，则 Unidrv 不会进行压缩。 此默认值与不具有位图字体压缩功能的较旧版本的 Unidrv 保持兼容。 仅当打印机支持位图字体 compressionThe 压缩位图字符数据采用压缩的运行时间长度的行重复格式时，才应将此属性设置为 **TRUE** 。

### <a name="usemode5compression"></a>UseMode5Compression?

**UseMode5Compression？** 属性控制 UniDrv 是否应使用模式5压缩。 模式 5 (或方法 5) 压缩是自适应压缩，它允许结合使用多种其他压缩 (方法，如未编码、TIFF 或增量行) 。 **UseMode5Compression？** 的默认值为**FALSE**，这意味着如果 GPD 中不存在此属性，则 Unidrv 不会执行自适应压缩。 此默认值将保持与较旧版本的 Unidrv 的兼容性，这些版本没有自适应压缩功能。 仅当打印机支持自适应压缩时，才应将此属性设置为 **TRUE** 。

### <a name="usehpglpolylineencoding"></a>UseHPGLPolylineEncoding?

**UseHPGLPolylineEncoding？** 属性控制 Unidrv 是否应使用折线编码。 HP-GL/2 支持笔向上/向下/向下/向下绘制/绘制相对于绘图向量的相对命令。  (PE) 命令编码的折线是表示向量的更高效方法。

**UseHPGLPolylineEncoding**的默认值为**FALSE**，这意味着如果 GPD 中不存在此属性，UNIDRV 将不使用 PE 命令。 此默认值保持与早期版本的 Unidrv 的兼容性，这些版本不支持 PE 命令。 仅当打印机支持折线编码时，才应将此值设置为 **TRUE** 。

### <a name="printschemaprivatenamespaceuri"></a>PrintSchemaPrivateNamespaceURI

**PrintSchemaPrivateNamespaceURI**特性定义核心驱动程序用于公开 PrintTicket 或 PrintCapabilities 中的私有 PPD 功能或选项的专用命名空间 URI。 该属性必须出现在 GPD 文档的根目录中，并包含将用于定义 Printticket 和 PrintCapabilities 文档中的命名空间的 URI 的 ASCII 表示形式。 该 URI 反过来会与不具有到公共架构的显式映射的所有功能和选项关联，或者核心驱动程序无法识别。

### <a name="printschemakeywordmap"></a>PrintSchemaKeywordMap

**PrintSchemaKeywordMap**属性显示在 GPD 文件中的功能和选项构造下。 此属性指示应在打印机定义的功能中使用的公共打印架构名称。 您可以通过使用 **PrintSchemaKeywordMap** 属性，重命名在 PrintTicket 中指定的任何选项（在 GPD 文件中除外和 Collate 除外）。

**注意**   对于显式识别的功能（包括页面大小和颜色），GPD 分析器将忽略此属性。

 

所有值都应该用引号引起来。 它们将使用 GPD 中指定的代码页（如果有）转换为 Unicode。 任何属性的重复定义的解析方式与其他 GPD 属性相同：将优先处理读取的最后一个定义。

**重要提示**   如果将功能映射到已在 GPD 文件中使用的 Print Schema 关键字，则相应的 PrintCapabilities 文档可能会多次列出该功能。 多次出现可能会造成混淆，因此不应将功能映射到 GPD 文件中使用的打印架构关键字。

 

**注意**   GPD 分析器会自动生成 InputBin 功能的 FORMSOURCE 选项，并将其映射到打印架构中的 "自动选择" 关键字。 如果 GPD 文件包含 InputBin 选项，该选项使用 **PrintSchemaKeywordMap** 属性将选项映射到 print schema 关键字，则打印架构中的功能将在设备命名空间中包含 FORMSOURCE 选项。 "自动选择" 将显示在 PrintCapabilities 文档中，并引用 GPD 文件的 **PrintSchemaKeywordMap** 属性中指定的选项。

 

下面的代码示例演示了用于显示布局的部分 GPD 文件。

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

可以为 Microsoft Win32 GDI 驱动程序和新的 [XPSDrv 驱动程序](xpsdrv-printer-drivers.md)使用 Windows Vista Unidrv 配置模块 ( # A0) 。 若要将 Unidrv 配置模块用于 XPSDrv 驱动程序，XPSDrv 驱动程序的 GPD 数据文件必须指定 **IsXPSDriver** 属性，并将其值设置为 **TRUE**。

例如，如果您有 XPS 驱动程序，请使用以下代码。

```cpp
*IsXPSDriver?: TRUE
```

若要将 Unidrv 配置模块用于 Win32 GDI 驱动程序，无需指定此属性。

### <a name="useimageforhatchbrush"></a>UseImageForHatchBrush?

**UseImageForHatchBrush？** 属性使用以下 GPD 语法。

```cpp
*Ifdef: WINNT_60
*UseImageForHatchBrush?: TRUE
*Endif: WINNT_60 
```

在 Microsoft Windows Server 2003 或 Windows XP 中，当 Unidrv 在 HP-UX/2 模式下进行打印时，如果 [**DrvRealizeBrush**](/windows/win32/api/winddi/nf-winddi-drvrealizebrush) 函数中收到影线画笔，则 Unidrv 将发送一个命令，以便打印机选择合适的阴影画笔。 Unidrv 不控制阴影画笔的呈现方式。 例如，行之间的间距通常由分辨率控制。 在较高的分辨率下，间距会变小，而在较低的分辨率下，间距会更大。 因此，如果使用不同的分辨率，文档可能会以不同的方式打印。

在 Windows Vista 中，如果 GPD 指定了 **UseImageForHatchBrush？** 属性，则 Unidrv 会将阴影画笔呈现到位图图面上，然后将该位图发送到设备。 因此，Unidrv 对阴影画笔的呈现方式有一些控制。

### <a name="reversebandorder"></a>ReverseBandOrder?

**ReverseBandOrder？** 属性使用以下 GPD 语法。

```cpp
*Ifdef: WINNT_60
*ReverseBandOrder?: TRUE
*Endif: WINNT_60 
```

**ReverseBandOrder**的值为**TRUE**或**FALSE** ，指示是否启用了反向条带。 此属性会导致按相反的顺序进行分级。 例如，对于纵向页面，将从下到上（而不是从上到下）进行分级。

此属性实质上与 ReverseBandOrderForEvenPages？相同，不同之处在于即使双工不 (处于活动状态，也会考虑使用 **ReverseBandOrder？** 仅当双工在) **上时才有效，** 并且它适用于所有页 (**ReverseBandOrderForEvenPages？** 仅在) 的偶数页上工作。 有关如何使用**ReverseBandOrder？** 和其他相关信息的详细信息，请参阅 \* **ReverseBandOrderForEvenPages？**。 特别要注意的是，插件必须反转扫描行和扫描行中的位。

可以结合使用 \* ReverseBandOrderForEvenPages？和 \* **ReverseBandOrder？**。

如果仅将 **ReverseBandOrder** 设置为 **TRUE**，则将对所有页面反转条带。

如果仅将 **ReverseBandOrderForEvenPages** 设置为 **TRUE**，则在打印机打印双面时，对 pagesonly 进行反向分级。 如果未设置双工，则忽略 **ReverseBandOrderForEvenPages？** 设置。

如果设置了 **ReverseBandOrder？** 和 **ReverseBandOrderForEvenPages？** ，则会发生以下情况：

-   如果双工处于开启，则为奇数页（ (为1、3、5、7等) 执行反向分级。

-   如果双工处于关闭状态，则对所有页面执行反向分级。

### <a name="bidiqueryfile"></a>BidiQueryFile

**BidiQueryFile**属性使用以下 GPD 语法。

```cpp
*BidiQueryFile: <GPD or GDL file name>
```

使用 **BidiQueryFile** 指定 GPD 或 GDL 文件名，其中包含打印机驱动程序的自动配置 **BidiQuery** 或 **BidiResponse** 数据。 GPD 或 GDL 文件名不应指定任何路径。 如果自动配置数据包含在驱动程序的数据文件 GPD 文件中，还可以将该 GPD 文件指定为 **BidiQueryFile** 特性的值。

下面的代码示例显示了一个部分 GPD 文件中的此属性的示例。

```cpp
*Ifdef: WINNT_60
*BidiQueryFile: "ACnfgUni.GDL"
*Endif: WINNT_60
```

 

