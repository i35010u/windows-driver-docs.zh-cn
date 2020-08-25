---
title: 预分析基础结构
description: 预分析基础结构
ms.assetid: 4c07145a-9a08-4507-8bab-769617e73d77
keywords:
- 分级 WDK Unidrv
- preanalysis 基础结构 WDK Unidrv
- 黑带 WDK Unidrv
- DrvStretchBlt
- OEMStretchBlt
- DrvStartBanding
- DrvNextBand
- DrvQueryPerBandInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2af7cebd85bed1b28ba87af9fa9ec334e4951666
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802553"
---
# <a name="preanalysis-infrastructure"></a>预分析基础结构





Preanalysis 基础结构是一种机制，用于在打印作业上强制分级，使每个页面的第一条带区重播是包含整个页面的带区。 Preanalysis pass 不允许进行任何呈现，并且仅在呈现对象之前，启用对页面上对象的分析。

若要允许整页 preanalysis，Unidrv 首先在 [**DrvEnableSurface**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablesurface) 函数中指定一个整页设备图面，然后通过 [*DrvQueryPerBandInfo*](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvqueryperbandinfo)指示第一个带区是整个页面的大小。 Preanalysis 完成后，Unidrv 将使用 *DrvQueryPerBandInfo* 将剪辑区域恢复到其大小，然后再启用 preanalysis;Unidrv 随后呈现到该表面。 由于 GDI 的实现限制，仅当 N 向上模式为 1 \_ 或呈现带区为整个页面时，才可以启用 preanalysis。

下面的伪代码演示了用于 preanalysis 的逻辑。

```cpp
DrvEnableSurface
if( preanalysis enabled )
   Use dummy device surface
DrvStartDoc
For each physical page 
{
   DrvStartPage
   DrvStartBanding
   For each banding surface 
   {
      DrvQueryPerBandInfo
// Set sizlBand member of PERBANDINFO
      if( preanalysis_pass ) 
         pbi.sizlBand = {whole page}
      else 
         pbi.sizlBand = {normal band}
      Carry out rendering operations
      if ( ( preanalysis pass && OEM preanalysis enabled ) || !preanalysis_pass ) {
         Call OEM hooks
         DrvNextBand
      }
      if ( ( preanalysis pass && OEM preanalysis enabled ) || !preanalysis_pass )
         Call OEMNextBand
      if( preanalysis pass ) {
         Disable preanalysis
         Switch from dummy device surface to real device surface
      }
      if( last band ) 
         Write end page character from GPD
   }  // for each banding surface

}  // for each physical page
DrvEndDoc
```

由于 preanalysis 功能必须适用于当前的一般打印机说明 (GPD) 文件和插件，因此，文本 z 顺序、空白带检测和其他操作都是从微型驱动程序的角度以不可见的方式实现的。 微型驱动程序可以挂钩 [**DrvStartBanding**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartbanding) 和 [**DrvNextBand**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvnextband)，但它不会收到第一次调用 **DrvNextBand** ，因为对 **DrvNextBand** 的第一次调用不包含任何呈现。 仅当插件在 GPD 中设置**DrvNextBand**标志来启用 OEM 对象级 preanalysis (\* **PreAnalysisOptions**： 8) 时，才会收到第一次 DrvNextBand 调用。 在这种情况下，插件必须挂钩**DrvStartBanding**和**DrvNextBand**，并且该插件必须检查**DrvStartBanding**函数的*pptl*参数。 如果 *pptl* 参数为非**NULL**，则将禁用 preanalysis。 如果 *pptl* 参数为 **NULL**，则指示 preanalysis 传递的开头。 在这种情况下，该插件应假设插件对所有绘图 DDIs 的调用都具有与 preanalysis 传递的挂钩结果。 Preanalysis pass 在第一次调用 **DrvNextBand** 函数时结束，并且在首次调用 **DrvNextBand** 函数后开始呈现。 对此函数的后续调用将包含呈现数据。

### <a name="preanalysisoptions-modes"></a><a href="" id="-preanalysisoptions-modes"></a>\*PreAnalysisOptions 模式

Preanalysis 模式由 \* **PreAnalysisOptions**： *n* attribute NAME 和 attribute 参数在 GPD 文件中进行控制。 下表列出了可与 \* **PreAnalysisOptions**属性名称一起使用的参数值。 可以组合使用这些值中的两个或更多来启用多个选项。

参数含义值0

禁用所有 preanalysis 模式。

1

默认模式。 启用 "单色 z 顺序文本分析" 和 "空白带优化"。 对于具有可下载字体或设备字体支持的设备，以及高分辨率 (600 dpi 或更高分辨率) 24 BPP 渲染模式，会启用此模式。

2

为 24 BPP [**IPrintOemUni：： ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing) 回调启用 1 bpp 优化。

4

启用设备 StretchBlt 操作。

8

启用 OEM 对象级别的 preanalysis。

 

### <a name="monochrome-z-order-text-analysis-with-blank-band-optimization"></a>带空格优化的单色 Z 顺序文本分析

```cpp
*PreAnalysisOptions: 1
```

如果将 \* **PreAnalysisOptions**参数设置为1，则 Unidrv 可以执行以下操作：

-   检测单色打印机中文本和图形对象之间的 z 顺序问题。

-   执行空白带优化。

第一个操作处理在以后覆盖下载到单色打印机的文本或与图形对象交互时出现的 z 顺序问题。 Z 顺序问题通常是由于图形对象所致，其中包含复杂的剪辑，因此 Unidrv 无法下载清除以前下载的文本的白色矩形。

Unidrv 在每一页上执行一次 preanalysis，然后再执行呈现处理。 Unidrv 执行此来确定是否将使用位块传输 (blt) 对象的任何文本与不能模拟的复杂剪辑重叠。 因此，文本呈现到 surface 位图上，而不是直接下载，这样以后呈现的对象将与文本正确交互。

此外，对于不支持白色矩形的设备，Unidrv 会检查是否有 blts 所覆盖的任何文本，即使它们不包含复杂剪辑也是如此。 Unidrv 在表面上呈现文本，而不是将其直接下载到打印机。

以下绘图命令针对可能由后续 blts 重叠的文本进行测试：

-   [**DrvBitBlt**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvbitblt)

-   [**DrvStretchBlt**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstretchblt)

-   [**DrvStretchBltROP**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstretchbltrop)

-   [**DrvStrokeAndFillPath**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstrokeandfillpath)

因此，此模式应该更正文本和填充区域对象之间的所有 z 顺序问题。 请注意，文本和重叠线条仍可能出现问题。 这种情况不包括在内，因为此类解决方案可能会导致下载几乎所有文本，而不是进行绘制。

此功能不能更正与使用设备字体关联的 z 顺序问题。 如果应用程序或驱动程序已选择设备字体模式，驱动程序将无法纠正此问题，并且无法将设备字体呈现到表面上。

第二个操作允许 Unidrv 优化页面上的空白区域。 在此模式下，Unidrv 将跳过空的上边距和下边距，以及该页中间的任何大空白区域。 此模式适用于彩色打印，可通过最大程度地减少呈现页面所需的频带数量，提高性能。

在 preanalysis 传递期间，Unidrv 确定页面上绘图的位置。 只要启用了 preanalysis，或者在高分辨率 (600 dpi 或更高) 的情况下打印机使用 24 BPP 呈现带区，就会启用空白带优化。这会使喷墨打印机的 24 BPP 渲染性能明显提高，并且无需更改现有的 OEM 插件。

### <a name="black-band-optimization"></a>黑带优化

```cpp
*PreAnalysisOptions: 2  *% 1 bpp ImageProcessing bitmaps
```

如果将 \* **PreAnalysisOptions**参数设置为2，则 Unidrv 可以使用更大的 1 BPP 条带区来呈现只包含实心黑色对象的区域，而不是将整个页面渲染为 24 BPP。 此模式类似于空带优化，但它还确定了纯黑色区域 (相对于页面上的颜色区域) 。 只有纯 (黑色的对象才会在 1 BPP 条纹面上呈现) ，因为在 1 BPP 单色中，为 24 BPP 颜色设置的半色调不会正确呈现。

Unidrv 在 [**DrvEnableSurface**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablesurface) 函数内创建两个图面：一个用于颜色，另一个用于 1 BPP 单色。 Unidrv 对每个使用相同的内存，因此不需要额外的内存。 页面 preanalysis 决定页面是否包含纯黑色或空白区域，对于包含颜色的区域，可以使用更大的带区。 只有颜色区域需要使用较小的色带图面。

使用相同的内存量，1 BPP 单色表面的大小可以等于 24 BPP 彩色面。 因此，仅在页面中间包含颜色的图像可以分为三个区域：顶区域、包含颜色的区域和底部区域。 这三个区域可以是镶边的，如下所示：顶级区域可以放置在单个单色带区中，包含颜色的区域可以分为多个颜色带区，以满足该区域的需要，底部区域可以放入单个单色带区。

此功能要求 Oem 支持 **IPrintOemUni：： ImageProcessing** 回调并处理光栅数据的转储。 对于 **IPrintOemUni：： ImageProcessing** 回调，当前的 OEM 插件支持必须得到增强，以接受 24 bpp 条带或 1 bpp 纯黑色条带。

### <a name="support-for-device-stretchblt-operations"></a>支持设备 StretchBlt 操作

```cpp
*PreAnalysisOptions: 4
```

将 \* **PreAnalysisOptions**参数设置为4可允许 Unidrv 将[**DrvStretchBlt**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstretchblt)调用直接下载到支持 stretchblt 操作的设备。

当 Unidrv 生成 24 BPP 彩色数据时，会将所有 stretchblt 图像拉伸到设备的分辨率，这将导致必须下载的光栅数据量非常大。 这可能会导致性能降低，还会导致许多东亚打印机上的内存不足的情况。

需要使用微型驱动程序 render 插件来利用 stretchblt 模式，因为它必须挂钩 [**OEMStretchBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/nf-printoem-oemstretchblt) 并提供自己的映像下载命令。 Unidrv 仅允许 OEMStretchBlt 挂钩到可以直接下载的调用。 因此，该插件不负责处理 z 顺序问题。 插件仅需直接下载它收到的 OEMStretchBlt 调用中包含的源映像数据。 如果图像采用的是插件不支持或无法下载的格式，则插件还可以选择将该图像 punting 为 Unidrv。

当直接将对象下载到设备，而在系统上呈现其他数据时，可能存在 z 顺序问题或半色调不一致。 此模式使用 preanalysis 来确定哪些 stretchblts 可直接下载。 仅不包含掩码或复杂剪辑的 stretchblts 将被视为直接下载。 如果后续对象覆盖了任何被视为直接下载的 stretchblts，则不会直接下载任何对象。 此原则应提高性能，并确保没有图像包括来自系统和设备的半色调，这会导致质量较差的打印输出。

### <a name="oem-object-level-preanalysis-hooks"></a>OEM 对象级 Preanalysis 挂钩

```cpp
*PreAnalysisOptions: 8
```

如果将 \* **PreAnalysisOptions**参数设置为8，则 OEM 可以启动 preanalysis pass，以便在[**DrvStartBanding**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartbanding)调用后播放整个页面上的所有对象，而不考虑带区大小。 在 preanalysis 期间，Unidrv 内不允许使用绘图，但 Oem 可以挂钩所有 DrvXxx 绘图调用来分析页面上的对象。

此模式中的功能侧重于彩色喷墨打印机，使 Oem 可以使用基于对象的颜色校正或呈现。 例如，如果特定打印机与颜色对象（而不是自身显示的黑色对象）相交，则需要以不同方式处理黑色对象。 其他 Oem 可能需要 stretchblt 对象的半色调，这与 bitblt 对象不同。 Stretchblt 对象可以采用 Windows 支持的任何图形文件格式，如 .png 或 .jpg。 Bitblt 对象只是位图。

如果在 GPD 中启用了此模式，则 Unidrv 会将曲面定义为条带图面，但会导致第一次播放为整个页面。 为此，Unidrv 会将 "GDI 剪辑" 窗口设置为整个页面。 Unidrv 允许挂钩所有绘图命令，但在执行任何绘制之前返回。 在以下情况下，Unidrv 会将剪辑窗口重置为正常的带区大小和带区。

如果 Oem 在 GPD 中启用了此模式，则需要将 **DrvStartBanding** 和 [**DrvNextBand**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvnextband) 挂钩。 它们必须测试**DrvStartBanding**函数的*pptl*参数，以确定 Unidrv 是否可以在指定页上启用此模式下的 preanalysis。 如果 *pptl* 参数为 **NULL**，则 Unidrv 已启用 preanalysis。 Unidrv 使用 *pptl* 参数，因为它目前没有任何意义， (未使用带区位置对其进行更新。 对于 preanalysis，带区位置始终设置为 (0，0) # A2。 如果 *pptl* 参数为 **NULL**，则 OEM 应将第一个 **DrvNextBand** 之前的所有绘图调用视为 preanalysis 的一部分，并且应允许不在图面上绘制。

Preanalysis 的结尾通过调用 **OEMNextBand** 函数发出信号。 传递给**OEMNextBand**的*pptl*参数不为**NULL**。 此调用仅用于将相应的 *pptl* 值返回给 Unidrv。 插件可以自行设置 *pptl* 值，也可以回叫 Unidrv (如本主题开头部分的伪代码示例所) 。 因为在第一次调用**OEMNextBand**时指定的**OEMNextBand**的*pso*参数尚未呈现，所以插件不应将其内容发送到设备。

 

 




