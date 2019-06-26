---
title: 预分析基础结构
description: 预分析基础结构
ms.assetid: 4c07145a-9a08-4507-8bab-769617e73d77
keywords:
- 具有带区 WDK Unidrv
- preanalysis 基础结构 WDK Unidrv
- 黑色带区 WDK Unidrv
- DrvStretchBlt
- OEMStretchBlt
- DrvStartBanding
- DrvNextBand
- DrvQueryPerBandInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f0064a37baaaf7c7f57cfa0cd68677eb6afc13d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373797"
---
# <a name="preanalysis-infrastructure"></a>预分析基础结构





Preanalysis 基础结构是一种机制，依据 Unidrv 强制条带的打印作业，以便每个页面的第一个外重播带区包含整个页面。 Preanalysis pass 将不允许任何呈现并完成只是为了支持分析页面上的对象的呈现对象之前。

若要允许整页 preanalysis，Unidrv 首先指定内的整页设备表面[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)函数，然后指示第一个带区，是通过方法整页的大小[ *DrvQueryPerBandInfo*](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo)。 Preanalysis 后使用完成后，Unidrv *DrvQueryPerBandInfo*的剪辑区域还原回其大小，启用 preanalysis; 之前Unidrv 随后将呈现给该图面。 由于实现的 GDI 的限制，仅当每张多模式是一个可以启用 preanalysis\_最多，或如果呈现带区整个页面。

下面的伪代码说明了用于 preanalysis 的逻辑。

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

由于 preanalysis 功能必须处理的当前通用打印机说明 (GPD) 文件，并且插件、 文本 z 顺序、 空白外检测和其他操作从微型驱动程序的角度来实现不可见的方式。 微型驱动程序可挂接[ **DrvStartBanding** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding)并[ **DrvNextBand**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)，但它将接收到的第一个调用**DrvNextBand**因为的首次调用到**DrvNextBand**不包括任何呈现。 插件收到第一个**DrvNextBand**它使 OEM 对象级 preanalysis GPD 中设置标志时才调用 (\***PreAnalysisOptions**:8). 在这种情况下该插件必须挂接**DrvStartBanding**并**DrvNextBand**，并且插件必须检查*pptl*参数**DrvStartBanding**函数。 如果*pptl*参数为非**NULL**，preanalysis 被禁用。 如果*pptl*参数是**NULL**，指示 preanalysis 阶段开始。 在这种情况下该插件应假定所有绘制 DDIs 插件具有挂接到调用源自 preanalysis 传递。 Preanalysis 传递结尾首次调用**DrvNextBand**函数，并呈现阶段开始后首次调用**DrvNextBand**函数。 对此函数的后续调用将包含呈现数据。

### <a href="" id="-preanalysisoptions-modes"></a>\*PreAnalysisOptions 模式

Preanalysis 模式控制 GPD 文件中\* **PreAnalysisOptions**: *n*属性名称和属性参数。 下表列出了可用于参数值\* **PreAnalysisOptions**属性名称。 可以组合两个或多个值，以启用多个选项。

参数的含义值 0

禁用所有 preanalysis 模式。

1

默认模式。 启用单色的 z 顺序的文本分析和空白外优化。 有关使用可下载的字体或设备字体支持和高分辨率设备启用此模式 (600 dpi 或更高版本)、 24 BPP 呈现模式。

2

启用 1 BPP 优化为 24 BPP [ **IPrintOemUni::ImageProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)回调。

4

启用设备 StretchBlt 操作。

8

启用 OEM 对象级 preanalysis。

 

### <a name="monochrome-z-order-text-analysis-with-blank-band-optimization"></a>使用空白外优化单色的 Z 顺序文本分析

```cpp
*PreAnalysisOptions: 1
```

设置\* **PreAnalysisOptions**参数为 1，Unidrv 来执行以下操作：

-   检测文本和单色打印机中的图形对象之间的 z 顺序中的问题。

-   执行空白外优化。

第一个操作处理出现时下载到单色打印机的文本更高版本覆盖或图形对象与之交互的 z 顺序问题。 Z 顺序问题通常是由包含复杂的剪辑，因此，Unidrv 是无法下载清除以前下载的文本的白色矩形的图形对象引起的。

之前其执行的呈现处理过程，Unidrv 每一页上执行 preanalysis 传递。 Unidrv 这样做是为了确定是否将使用不能模拟复杂剪辑的位块传输 (blt) 对象使用叠加的任何文本。 因此，而不是正在直接下载，以便更高版本呈现的对象并将文本与正确交互图面上的位图上呈现的文本。

此外，对于不支持白色矩形的设备，Unidrv 检查叠加的 blts，即使它们不包含复杂的剪辑的任何文本。 Unidrv 呈现的文本而不是将其下载到打印机直接在图面。

以下的绘图命令是针对可能由后续 blts 叠加的文本进行测试：

-   [**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)

-   [**DrvStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)

-   [**DrvStretchBltROP**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)

-   [**DrvStrokeAndFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)

因此，此模式下，应更正的文本与填充区域对象之间的所有 z 顺序问题。 请注意，可以仍有问题的文本和重叠的行。 这种情况下不包括，因为此类解决方案可能会导致正在下载而不是所绘制的几乎所有文本。

此功能无法解决与使用设备字体的 z 顺序问题。 如果应用程序或驱动程序，已选中设备字体模式，该驱动程序不能更正此问题，将不能呈现到图面上的设备字体。

第二个操作允许 Unidrv 可优化页面上的空白区域。 在此模式下，Unidrv 跳过空顶部和底部边距，以及在页面中间的任何大型空白区域。 此模式下，其目的是在彩色打印中使用，将呈现的页面所需的带外传递数降至最低，以提高性能。

Preanalysis 阶段 Unidrv 确定绘图页上发生。 每当启用 preanalysis，或打印机使用高分辨率的 24 BPP 呈现带区时启用了空白外优化 (600 dpi 或更高版本)。这应该导致喷墨打印机 24 BPP 呈现较显著的性能提升，无需更改对现有 OEM 插件。

### <a name="black-band-optimization"></a>黑色外优化

```cpp
*PreAnalysisOptions: 2  *% 1 bpp ImageProcessing bitmaps
```

设置\* **PreAnalysisOptions**参数为 2 允许 Unidrv 使用更大 1 BPP 条带面，可用来呈现区域只包含纯黑色对象，而不是呈现整个页面在 24 BPP。 此模式非常类似于空白外优化，它还确定实体的黑色区域 （而不是颜色区域） 的页上出现异常。 仅是纯黑色 （没有灰色底纹） 的对象可以呈现在 1 BPP 条带图面，因为半色调为 24 BPP 颜色设置不在 1 BPP 单色中正确呈现。

Unidrv 创建中的两个面[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)函数： 一个用于颜色，另一个用于 1 BPP 单色。 Unidrv 对于每个，使用相同的内存，因此不不需要任何额外的内存。 页 preanalysis 确定页是否包含实体的黑色或空白区域，为其较大的带区可用于与包含颜色的区域。 仅在颜色区域需要使用较小的颜色外面。

使用相同量，1 BPP 单色图面可以是内存的 24 再乘以多达 24 BPP 颜色图面。 因此，包含仅在页面中间颜色的图像可以划分为三个区域： 顶部区域、 包含颜色的区域和底部区域。 以下三个区域可以具有按如下所示的带区： 顶部区域可放置在单个单色外、 包含颜色的区域可以分为多颜色带区根据需要覆盖它，和底部区域可以放入单个单色外。

此功能需要支持的 Oem **IPrintOemUni::ImageProcessing**回调并处理光栅数据的转储。 支持插件的当前 OEM **IPrintOemUni::ImageProcessing**回调必须改进为接受 24 BPP 带区或 1 BPP solid 黑带区。

### <a name="support-for-device-stretchblt-operations"></a>对设备 StretchBlt 操作的支持

```cpp
*PreAnalysisOptions: 4
```

设置\* **PreAnalysisOptions**为 4 的参数允许 Unidrv 下载[ **DrvStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)直接对设备调用该支持 stretchblt操作。

当 Unidrv 生成 24 BPP 颜色数据时，所有 stretchblt 图像将都拉伸到设备，这会导致大量必须下载的光栅数据的分辨率。 这可能导致性能降低，除了许多东亚打印机上的内存不足条件。

微型驱动程序呈现插件需要充分利用 stretchblt 模式，因为它必须挂接[ **OEMStretchBlt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/nf-printoem-oemstretchblt)并提供自己的映像下载命令。 Unidrv 允许仅在调用，可直接下载 OEMStretchBlt 挂钩。 因此，该插件不负责处理 z 顺序问题。 插件只需直接下载它收到的 OEMStretchBlt 调用中包含的源映像数据。 该插件还可以选择回 Unidrv punting 图像，如果图像是一种格式，该插件不支持或不能下载。

每次对象直接下载到设备的其他数据呈现在系统上时，可以有 z 顺序的问题或半色调的不一致。 此模式下使用 preanalysis 来确定哪些 stretchblts 可以直接下载。 不包含掩码或复杂的剪辑的 stretchblts 将考虑直接下载。 如果更高版本的对象覆盖任何直接下载，则没有对象正在被视为 stretchblts 将会直接下载。 这一原则应提高性能，并应确保没有图像包含半色调从这两个系统和设备，这会导致非常不佳质量的打印输出。

### <a name="oem-object-level-preanalysis-hooks"></a>OEM 对象级 Preanalysis 挂钩

```cpp
*PreAnalysisOptions: 8
```

设置\* **PreAnalysisOptions**为 8 的参数允许 OEM 启动 preanalysis 传递，以便在整个页面上的对象的所有播放后[ **DrvStartBanding**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding)调用而不考虑带区大小。 没有绘图中允许包含 Unidrv preanalysis 阶段，但 Oem 可以挂接所有 DrvXxx 绘制调用，以分析页面上的对象。

在此模式下的功能被侧重于颜色喷墨打印机，以便 Oem 可以使用基于对象的颜色校正或呈现。 例如，某些打印机需要以不同方式处理黑色对象，如果它们与颜色对象，而不是单独出现的黑色对象相交。 其他 Oem 的 stretchblt 对象不同于 bitblt 对象可能需要半色调。 Stretchblt 对象可以是 Windows 支持，例如.png 或.jpg 任何图形文件格式。 Bitblt 对象是以独占方式位图。

GPD 中启用此模式，Unidrv 作为联合的图面上，定义在图面，但会导致整个页面的第一个播放。 若要执行此操作，Unidrv 将 GDI 剪辑窗口设置为整个页面中。 Unidrv 允许所有绘图命令使用户被挂起，但是，可以执行任何绘图之前返回。 以下传递 Unidrv 将重置剪辑窗口返回到正常的带区大小和带区像往常一样。

Oem 必须挂接两者**DrvStartBanding**并[ **DrvNextBand** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)时它们已经启用了 GPD 中的此模式。 他们必须测试*pptl*的参数**DrvStartBanding**函数来确定是否 Unidrv 可以启用 preanalysis 在此模式下指定的页。 如果*pptl*参数是**NULL**，则 Unidrv 已启用 preanalysis。 使用 Unidrv *pptl*参数因为它没有任何意义此时 （它尚未更新外位置。 对于 preanalysis 外, 位置始终设置为 （0，0）)。 如果*pptl*参数是**NULL**，则 OEM 应考虑在第一个之前的所有绘图调用**DrvNextBand**是 preanalysis 的一部分，应允许任何绘图在图面。

通过调用发出信号 preanalysis 末尾**OEMNextBand**函数。 *Pptl*参数传递给**OEMNextBand**不是**NULL**。 此调用仅用于返回适当*pptl* Unidrv 的值。 插件可以设置*pptl*值本身也可以调用返回到 Unidrv （如本主题开头前面的伪代码示例那样）。 因为条带作品*pso*的参数**OEMNextBand**首次调用中指定**OEMNextBand**具有尚未呈现，插件不应发送其到设备的内容。

 

 




