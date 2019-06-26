---
title: Windows 8 中的 DirectX 功能改进
description: Windows 8 包含 Microsoft DirectX 功能改进，开发人员、 最终用户和系统制造商中受益。
ms.assetid: 0622DA0D-41ED-4B47-B090-8D5B85E10EB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92560f67bfbd8a7522104b43eb899eba3a8b4bac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353458"
---
# <a name="directx-feature-improvements-in-windows-8"></a>Windows 8 中的 DirectX 功能改进


Windows 8 包含 Microsoft DirectX 功能改进，开发人员、 最终用户和系统制造商中受益。

功能改进包括以下几个方面：

-   [像素格式 (5551，565、 4444)](#pixelformats):在低功率硬件配置上的 DirectX 应用程序的更高的性能。
-   [双精度着色器功能](#dblshader):高级别着色器模型的性能改进，可执行更多操作不涉及 CPU 在 GPU 上。
-   [独立于目标的光栅化](#tir):Direct2D 应用程序更高性能的抗锯齿路径。
-   [不覆盖并丢弃](#noow):Microsoft Direct3D 11.1 移动平台和使用基于磁贴的呈现器的 power 约束设备上的应用程序的性能更高版本。
-   [在每个阶段的 Uav](#uav):若要启用着色器调试在 DirectX 11.1 硬件上的所有着色器阶段的添加的功能。
-   [跨进程共享的纹理阵列 （适用于支持立体 3D）](#stereo):提供了基础，若要启用立体三维效果。
-   [无序访问视图与多重采样抗锯齿示例访问](#unordered):使 Direct3D 11 应用程序以实现高质量呈现算法，而无需为大量的示例分配内存。
-   [逻辑 ops](#logicops):延迟的明暗度技术的改进。
-   [改进了常量缓冲区控制](#buffers):游戏开发人员的高效缓冲区管理。

## <a name="span-idpixelformatsspanspan-idpixelformatsspanpixel-formats-5551-565-4444"></a><span id="pixelformats"></span><span id="PIXELFORMATS"></span>像素格式 (5551，565、 4444)


若要更好地支持在低功耗配置中使用 DirectX 的图形，从以下的 DirectX 9 像素格式[ **DXGI\_格式**](https://docs.microsoft.com/windows/desktop/api/dxgiformat/ne-dxgiformat-dxgi_format)必须在 Direct3D 为中支持枚举Windows 8:

-   **DXGI\_FORMAT\_B5G6R5\_UNORM**
-   **DXGI\_FORMAT\_B5G5R5A1\_UNORM**
-   **DXGI\_FORMAT\_B4G4R4A4\_UNORM**

这些其他格式在 DirectX 应用程序中的低功率硬件上提供更高的性能。 到现在的所有 Gpu 都支持这些格式。 下表描述所需的支持，对于这些格式，具体取决于硬件功能级别。

**所需格式支持，具体取决于硬件功能级别**

| 功能                       | 功能级别 9\_x                                      | 功能级别 10.0                                             | 功能级别 10.1                        | 功能级别 11 +                         |
|----------------------------------|---------------------------------------------------------|----------------------------------------------------------------|-------------------------------------------|-------------------------------------------|
| 类型化的缓冲区                     | 否                                                      | 必需                                                       | 必需                                  | 必需                                  |
| 输入装配器顶点缓冲区    | 否                                                      | 可选                                                       | 可选                                  | 可选                                  |
| Texture1D                        | 否                                                      | 必需                                                       | 必需                                  | 必需                                  |
| Texture2D                        | 必需                                                | 必需                                                       | 必需                                  | 必需                                  |
| Texture3D                        | 否                                                      | 必需                                                       | 必需                                  | 必需                                  |
| TextureCube                      | 必需                                                | 必需                                                       | 必需                                  | 必需                                  |
| 着色器 ld\*                      | 否                                                      | 必需                                                       | 必需                                  | 必需                                  |
| 着色器示例\*（使用筛选） | 必需                                                | 必需                                                       | 必需                                  | 必需                                  |
| 着色器 gather4                   | 否                                                      | 否                                                             | 否                                        | 必需                                  |
| Mipmap                           | 必需                                                | 必需                                                       | 必需                                  | 必需                                  |
| Mipmap 自动生成           | 为 565 对于 4444，是可选的所需 5551               | 为 565 对于 4444，是可选的所需 5551                      | 为 565 对于 4444，是可选的所需 5551 | 为 565 对于 4444，是可选的所需 5551 |
| RenderTarget                     | 所需为 565，不适用于 4444 5551                     | 为 565 对于 4444，是可选的所需 5551                      | 为 565 对于 4444，是可选的所需 5551 | 为 565 对于 4444，是可选的所需 5551 |
| Blendable 呈现器目标           | 所需为 565，不适用于 4444 5551                     | 为 565 对于 4444，是可选的所需 5551                      | 为 565 对于 4444，是可选的所需 5551 | 为 565 对于 4444，是可选的所需 5551 |
| UAV 类型化的应用商店                  | 否                                                      | 否                                                             | 否                                        | 可选                                  |
| CPU 可锁定                     | 必需                                                | 必需                                                       | 必需                                  | 必需                                  |
| 4x MSAA                          | 可选                                                | 可选                                                       | 为 565 对于 4444，是可选的所需 5551 | 为 565 对于 4444，是可选的所需 5551 |
| 8x MSAA                          | 可选                                                | 可选                                                       | 可选                                  | 为 565 对于 4444，是可选的所需 5551 |
| 其他 MSAA 样本计数          | 可选                                                | 可选                                                       | 可选                                  | 可选                                  |
| 多重采样解析              | （如果支持 MSAA） 的针对所需为 565，否 4444，5551 | 所需为 565 对于 4444，是可选的 （如果支持 MSAA） 5551  | 为 565 对于 4444，是可选的所需 5551 | 为 565 对于 4444，是可选的所需 5551 |
| 多重采样负载                 | 否                                                      | 所需为 565 对于 4444，是可选的 （如果支持 MSAA） 5551) | 为 565 对于 4444，是可选的所需 5551 | 为 565 对于 4444，是可选的所需 5551 |

 

## <a name="span-iddblshaderspanspan-iddblshaderspandouble-precision-shader-functionality"></a><span id="dblshader"></span><span id="DBLSHADER"></span>双精度着色器功能


在 Windows 8 中，支持双精度的 Windows 显示器驱动程序模型 (WDDM) 1.2 驱动程序还必须支持其他双精度浮点指令在高级别着色器模型中 5 中所有着色器阶段。 说明是：

-   双精度倒数
-   双精度除
-   双精度融合在乘加

因为运行时可以这些说明将直接传递给驱动程序，实现可以优化其性能，或将它们实现为专用硬件中的单个说明进行操作。

**请注意**  若要使用这些功能，开发人员必须确保它们运行功能\_级别\_11 或更高版本与双精度支持 (D3D11\_功能\_双精度型值) 上WDDM 1.2 或更高版本的驱动程序。

 

### <a name="span-idsumofabsolutedifferencesspanspan-idsumofabsolutedifferencesspanspan-idsumofabsolutedifferencesspansum-of-absolute-differences"></a><span id="Sum_of_absolute_differences"></span><span id="sum_of_absolute_differences"></span><span id="SUM_OF_ABSOLUTE_DIFFERENCES"></span>绝对差的总和

图像处理是新式设备中的关键应用程序。 常见操作是模式匹配或搜索。 视频编码操作通常搜索匹配的正方形磁贴 （通常 8 x 8 或 16 x 16） 和图像识别算法搜索由一个位掩码的更多常规形状。 若要提高性能的这些情况下，新内部函数已添加到 Microsoft 高级着色器语言 (HLSL) 对着色器模型 5.0 中所有着色器阶段。 此内部函数 msad4() 对应于并在着色器 IL 中生成的绝对差异 (MSAD) 指令的掩码总和的组。 所有 WDDM 1.2 和更高版本的驱动程序必须都支持此指令直接在硬件中或为一系列 （模拟） 的其他说明。

**请注意**  因此该溢出导致饱和度，换行行为不在理想情况下，应实现 MSAD 指令。 请注意溢出行为是未定义。

开发人员必须检查以确保它们运行功能\_级别\_11 或更高版本上的 WDDM 1.2 或更高版本的驱动程序以使用此功能。 开发人员必须不依赖于溢出的累计值的结果准确性 （即，超过 65535）。

 

## <a name="span-idtirspanspan-idtirspantarget-independent-rasterization-tir"></a><span id="tir"></span><span id="TIR"></span>独立于目标的光栅化 (TIR)


独立于目标的光栅化 (TIR) 提供了 Direct2D 应用场景涉及高质量抗锯齿的结构化图形的高性能抗锯齿路径。 TIR 启用 Direct2D 将光栅化步骤从 CPU 到 GPU 时保留的 Direct2D 抗锯齿语义和质量。 使用此功能，软件层才能评估大量的子像素示例位置的覆盖范围，但仅分配的内存所需的较小数目的示例。 这提供了使用 GPU 来呈现，但保留 CPU 呈现实现的图像质量的性能优势。 这样，一个用于广播到多个样本的多重采样抗锯齿呈现器目标的单一示例。

### <a name="span-idsamplecount1limitedtiron1010111spanspan-idsamplecount1limitedtiron1010111spanspan-idsamplecount1limitedtiron1010111spansamplecount-1-limited-tir-on-10-101--11"></a><span id="SampleCount__1__Limited_TIR_on_10__10.1___11_"></span><span id="samplecount__1__limited_tir_on_10__10.1___11_"></span><span id="SAMPLECOUNT__1__LIMITED_TIR_ON_10__10.1___11_"></span>SampleCount = 1 (10，10.1 及 11 有限 TIR)

Direct3D 10.0 的 Direct3D 11.0 硬件 (和功能级别 10\_0-11\_0) 支持 ForcedSampleCount 设置为 1 （和呈现目标视图任何示例计数） 以及所述的限制 （例如，没有深度/模具）。

适用于 10\_0，10\_1 和 11\_0 硬件，当[ **D3D11\_1\_DDI\_光栅器\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11_1_ddi_rasterizer_desc)。**ForcedSampleCount**设置为 1，行呈现不能配置为 2 的三角形 （四边形） 的基于模式 (即**MultisampleEnable**状态无法设置为 true)。 此限制不存在适用于 11\_1 的硬件。 请注意的命名**MultisampleEnable**状态有误导性，因为它不再具有启用多重采样执行任何操作; 相反，它是现在一起使用的控件之一**AntialiasedLineEnable**用于选择行呈现模式。

这与限制的独立于目标的光栅化窗体**ForcedSampleCount** = 1，与 Direct3D 10.0 中已存在但 Direct3D 10.1 和 Direct3D 变得不可用的模式相符 (和功能级别 10\_1 和 11\_0) 由于 API 进行了更改。 Direct3D 10.0 中此模式为中心采样即使在已可用的多个采样抗锯齿 (MSAA) 表面上呈现**MultisampleEnable**设置为 false (这可以通过切换切换和**MultisampleEnable**)。 在 Direct3D 中 10.1 + **MultisampleEnable**不再影响多重采样 （尽管名称），并仅控制行呈现行为。

## <a name="span-idnoowspanspan-idnoowspanno-overwrite-and-discard"></a><span id="noow"></span><span id="NOOW"></span>不覆盖并丢弃


### <a name="span-idrenderingcontentonatile-baseddeferred-renderingtbdrarchitecturespanspan-idrenderingcontentonatile-baseddeferred-renderingtbdrarchitecturespanspan-idrenderingcontentonatile-baseddeferred-renderingtbdrarchitecturespanrendering-content-on-a-tile-based-deferred-rendering-tbdr-architecture"></a><span id="Rendering_content_on_a_tile-based_deferred-rendering__TBDR__architecture"></span><span id="rendering_content_on_a_tile-based_deferred-rendering__tbdr__architecture"></span><span id="RENDERING_CONTENT_ON_A_TILE-BASED_DEFERRED-RENDERING__TBDR__ARCHITECTURE"></span>呈现内容在基于磁贴的延迟呈现 (TBDR) 体系结构

通过使用一组新的资源 Api 呈现 Direct3D 11.1 可以现在支持中的目标放弃行为。 开发人员必须了解此功能，并调用其他 Discard() 方法更高效地 TBDR 体系结构上运行 （与传统图形硬件无损失）。 这将提高移动平台和使用平铺的呈现器的其他电源受限设备上的性能。

### <a name="span-idupdatingresourcesonatbdrarchitecturespanspan-idupdatingresourcesonatbdrarchitecturespanspan-idupdatingresourcesonatbdrarchitecturespanupdating-resources-on-a-tbdr-architecture"></a><span id="Updating_resources_on_a_TBDR_architecture"></span><span id="updating_resources_on_a_tbdr_architecture"></span><span id="UPDATING_RESOURCES_ON_A_TBDR_ARCHITECTURE"></span>正在更新 TBDR 体系结构上的资源

由于 TBDR 体系结构通过相同的命令缓冲区完成多个阶段，必须使用特别留意要通知的驱动程序时的子资源部分未进行修改在上一个绘图调用过程。 具有无\_Direct3D 上的覆盖使用率**UpdateSubResource**函数可帮助管理资源对纹理的区域进行任何以前的绘图调用了其中的驱动程序。 这只需要通知应用程序的目的是放弃现有的数据，或不会重写保护的驱动程序。 这使 TBDR 体系结构上的更高效呈现，引入了任何损失，传统的桌面硬件上运行时。

这两个更新的 GPU 面部分，Direct3D 11 UpdateSubresource() 和 CopySubresourceRegions Api 的新变体在不提供添加标志字段\_，可以指定覆盖或丢弃。

这些 Api 推动的 Direct3D 11.1 设备驱动程序接口 (DDI) 和 Direct3D 9 DDIs。 通过添加此处讨论的标志来支持修订 BLT、 BUFBLT、 VOLBLT 和 TEXBLT DDIs 所需任何 DirectX 9 + 硬件的新驱动程序。

它们还需要支持所有 Direct3D 10 + 硬件与 Direct3D 11.1 驱动程序。

## <a name="span-iduavspanspan-iduavspanuavs-at-every-stage"></a><span id="uav"></span><span id="UAV"></span>在每个阶段的 Uav


在 Microsoft Direct3D 11 中，无序访问视图 (Uav) 数被限制为 8 的计算着色器处和至八个组合 (呈现目标视图 (RTVs) + Uav) 在像素着色器。 DirectX 11.1 中可以绑定数已增加。 有关 DirectCompute，现在限制为 64，并对图形为所有绑定的输出合并器为 64 （这就是，图形可以具有 64 减去向上-到-8 个可能使用的 RTVs）。

可以访问来自任何着色器阶段，但仍可从图形管道的总无序的访问视图

在每个着色器阶段添加 Uav，可将调试信息添加到管道。 此易于开发使 Windows 用于编写 GPU 加速应用程序更为理想平台。

这要求至少一个 DirectX 11.1 功能级别。

## <a name="span-idstereospanspan-idstereospancross-process-sharing-of-texture-arrays-for-supporting-stereoscopic-3-d"></a><span id="stereo"></span><span id="STEREO"></span>跨进程共享的纹理阵列 （适用于支持立体三维）


尽管立体三维是一项可选 WDDM 1.2 系统功能，但没有无论它们支持立体 3d 系统功能的所有 WDDM 1.2 设备驱动程序必须都实现的底层基础结构。

DirectX 10 （或更高版本） 的支持的图形硬件必须支持跨进程共享的纹理数组。 此功能提供了基础，若要启用立体三维效果。 WDDM 1.2 Direct3D DDIs 需要独立于硬件功能级别的呈现器目标作为数组缓冲区的支持。

此要求确保立体声的应用程序不会在 mono 模式下具有故障。 例如： 即使在系统上未启用立体声时应用程序应该能够创建立体声交换链或数组的缓冲区呈现器目标，然后调用**存在**。 在这种情况下，显示仅左的视图 (或者，如果*喜欢右* Microsoft DirectX 图形基础结构 (DXGI) 设置存在标志，则仅右视图)。

因此，WDDM 1.2 驱动程序 （所有的图形和渲染设备） 必须支持 Direct3D 11 Api，通过添加对跨进程共享的纹理数组的支持。 在早期版本中，跨进程共享的资源可能仅单层图面。 在 Windows 8 中的共享数组的最大大小为两个元素 （这已足够立体声）。 有关此要求的详细信息，请参阅**Device.Graphics...Stereoscopic3DArraySupport**中[Windows 硬件认证要求](https://go.microsoft.com/fwlink/p/?linkid=324537)。 其他相关的 Microsoft WindowsWindowsWindows HCK 要求均**Device.Graphics...ProcessingStereoscopicVideoContent**并**Device.Display.Monitor.Stereoscopic3DModes**。

## <a name="span-idunorderedspanspan-idunorderedspanuavs-with-multi-sample-anti-alias-sample-access"></a><span id="unordered"></span><span id="UNORDERED"></span>使用多重采样抗锯齿示例访问 Uav


Direct3D 11 允许光栅化到无序访问视图 (Uav) 与任何呈现目标视图 (RTVs) / Dsv 绑定。 即使 Uav 可以具有任意大小，该实现可以使用视区/剪刀矩形的像素尺寸运行光栅化程序。 DirectX 11 硬件的示例模式是只有单个示例。 DirectX 11.1 硬件规范将展开以允许多个样本。 这是独立于目标的光栅化的变体仅 Uav 绑定到的位置的输出。

仅限 UAV 的呈现以及在光栅化程序的多重采样是现在可以通过关闭 ForcedSampleCount 状态，限制为 0、 1、 4 和 8 （而不是 16，TIR 支持) 的示例模式键入。 （Uav 本身不是在分配方面多级采样。）设置为 0 等效于设置 1-单一样本光栅化。

着色器可以请求与仅限 UAV 的呈现的像素频率调用。 但是，请求采样频率调用是无效 （产生未定义的明暗度的结果）。 SampleMask 光栅器状态不影响此处光栅化行为。

对 DirectX 11.0 + 硬件，包括不支持完整 11 的硬件上提供了此功能的支持\_1 级别与 RTVs 独立于目标的光栅化。 该驱动程序可以报告它支持仅限 UAV 的多重采样抗锯齿示例访问 (MSAA) 呈现 （这意味着 4 和 8 示例同时支持）。 DirectX 11 + 的所有硬件都支持 1。 如果硬件可以执行完整 11\_1 独立于目标的光栅化使用 RTVs （它需要 16 示例支持），则需要 （即 4 和 8 示例在仅限 UAV 的情况下） 的仅限 UAV 的 MSAA 光栅化支持。

此功能使应用程序以实现高质量呈现算法，如分析的抗锯齿功能而无需为大量的示例分配内存。

## <a name="span-idlogicopsspanspan-idlogicopsspanlogic-operations"></a><span id="logicops"></span><span id="LOGICOPS"></span>逻辑操作


从而允许在输出合并器的逻辑操作，可对映像目前不可以执行一些操作。 例如，可以更有效地计算掩码，并轻松地还实现用于三维呈现的现代延迟的明暗度技术。

虽然此功能存在于大多数三维硬件，它不是当前通用的颜色混合原样。 因此，逻辑操作的配置存在一些约束通过以下方式：

-   第一个 RT blend desc 中使用的逻辑操作时, IndependentBlendEnable 必须设置为 false，以便相同的逻辑操作适用于所有 RTs。
-   当使用逻辑操作时，所有 RenderTargets 绑定必须都具有 UINT 或圣格式，否则呈现是不确定。

## <a name="span-idbuffersspanspan-idbuffersspanimproved-control-of-constant-buffers"></a><span id="buffers"></span><span id="BUFFERS"></span>改进的控制功能的常量缓冲区


### <a name="span-idpartialbufferspanspan-idpartialbufferspanpartial-constant-buffer-updates"></a><span id="partialbuffer"></span><span id="PARTIALBUFFER"></span>部分常量缓冲区更新

常量缓冲区如今在 clobber 整个缓冲区的更新过程，需要从源到目标的整体化副本。 其中我们想要更新仅为一部分的常量缓冲区写入的偏移量是理想之选。 这一能力为随机访问写入常量缓冲区到请求的游戏开发人员，并使常量缓冲区管理更自然且更高效。 这些功能已受支持的其他缓冲区类型，并添加到 WDDM 1.2 驱动程序中的常量缓冲区。

此功能必须支持的所有 Direct3D 10 + 硬件与 Direct3D 11.1 驱动程序。 对于开发人员，这是 DirectX 9 的硬件上模拟，因此它可以在所有功能级别。

**请注意**  必须指定 NO 任一\_覆盖或丢弃的标志。

 

### <a name="span-idoffsettingconstantbufferupdatesspanspan-idoffsettingconstantbufferupdatesspanspan-idoffsettingconstantbufferupdatesspanoffsetting-constant-buffer-updates"></a><span id="Offsetting_constant_buffer_updates"></span><span id="offsetting_constant_buffer_updates"></span><span id="OFFSETTING_CONSTANT_BUFFER_UPDATES"></span>偏移常量缓冲区更新

高性能游戏引擎为常见的需求之一是收集的常量引用的单独的常量缓冲区更新大批量**绘制\\** * 调用时，每次需要自己常量。 这得益于允许应用程序来创建较大的缓冲区，然后定位到区域中的单个着色器 (类似于视图，但无需使整个对象来描述视图)。

常量缓冲区现在可以创建具有大小大于可寻址的最大的常量缓冲区大小的单个着色器 （最多 4096 16 字节元素-65 kB，其中每个元素是一个四分量着色器常量）。 常量缓冲区资源大小现在仅受系统能够处理的内存分配的大小限制。

当大于 4096 元素的常量缓冲区绑定到管道通过使用 **\*SetShaderConstants**等 Api 就**VSSetShaderConstants**，它出现在着色器像它是仅 4096大小中的元素。

一个变体 **\*SetShaderConstants**Api，  **\*SetShaderConstants1**，允许"FirstConstant"和"ConstantCount"与绑定一起指定。 当由 ConstantCount （16 字节常量的数量） 定义常量缓冲区绑定这样一来，似乎像它开始偏移量 （其中 1 表示 16 字节） 指定"FirstConstant"并且其大小的着色器访问。 这基本上是一个轻型的较大的常量缓冲区的某一区域的"视图"。 （FirstConstant 和 ConstantCount 必须是 16 的倍数）。

此功能必须支持所有 WDDM 1.2 驱动程序的 Direct3D 10 + 硬件。 Direct3D 11 运行时为功能级别 9 模拟的适当行为\_x。

## <a name="span-idclearviewspanspan-idclearviewspanclearview"></a><span id="clearview"></span><span id="CLEARVIEW"></span>Clearview


此功能，要执行清除的单个 API/DDI 调用中的多个矩形的视频内存资源上有效的清除操作的实现。 该 API 包括对定义一部分的资源要清除的矩形的支持。 此功能支持 DirectX 9 DDI 中，需对 Windows 8 驱动程序 (WDDM 1.2)。 此方法会导致改进了性能的二维操作，例如所使用的图像处理和 UI。

## <a name="span-idcpyflagspanspan-idcpyflagspantileable-copy-flag"></a><span id="cpyflag"></span><span id="CPYFLAG"></span>Tileable 复制标志


Tileable 复制操作，以通知实现，图像源和目标都是像素对齐并不会参与后续呈现处理过程中的信息的跨像素 exchange 应用程序。 这样，在某些实现中它们都受益于在复制操作期间缓存的图像数据子集的显著的性能改进。 此功能支持 DirectX 9 DDI 中，需对 Windows 8 和更高版本的驱动程序 (WDDM 1.2)。

## <a name="span-idblitsspanspan-idblitsspansame-surface-blits"></a><span id="blits"></span><span id="BLITS"></span>同一个面 blits


许多 UI 操作，例如滚动时，需要将映像数据从一个图像的一部分传输到另一个。 此功能将添加对复制操作的源矩形和目标矩形位于同一个映像或资源的支持。 对于重叠的源和目标矩形，这种情况必须由实现和驱动程序正确处理。 这已要求使用 DirectX 9 DDI 和所需 WDDM 1.2 中的所有硬件。 此方法会导致显著的性能改进的主要 UI 方案。

## <a name="span-iddirect3d111ddispanspan-iddirect3d111ddispandirect3d-111-ddi"></a><span id="direct3d_11.1_ddi"></span><span id="DIRECT3D_11.1_DDI"></span>Direct3D 11.1 DDI


这些函数和结构是新的或更新 Windows 8:

-   [*AssignDebugBinary*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_assigndebugbinary)
-   [*CalcPrivateBlendStateSize(D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivateblendstatesize)
-   [*ClearView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_clearview)
-   [*DefaultConstantBufferUpdateSubresourceUP(D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_resourceupdatesubresourceup)
-   [*ResourceUpdateSubresourceUP(D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_resourceupdatesubresourceup)
-   [*VsSetConstantBuffers(D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_setconstantbuffers)
-   [**D3D11\_1DDI\_D3D11\_OPTIONS\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_d3d11_options_data)
-   [**D3DDDI\_BLTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_bltflags)
-   [**D3DDDI\_COPY\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-d3dddi_copy_flags)
-   [**D3DDDIARG\_BUFFERBLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_bufferblt1)
-   [**D3DDDIARG\_DISCARD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_discard)
-   [**D3DDDIARG\_TEXBLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_texblt1)
-   [**D3DDDIARG\_VOLUMEBLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_volumeblt1)
-   [**D3DDDICAPS\_体系结构\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddicaps_architecture_info)
-   [**D3DDDICAPS\_着色器\_MIN\_精度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-d3dddicaps_shader_min_precision)
-   [**D3DDDICAPS\_着色器\_MIN\_精度\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddicaps_shader_min_precision_support)
-   [**D3DDDICAPS\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddicaps_type)

 

 





