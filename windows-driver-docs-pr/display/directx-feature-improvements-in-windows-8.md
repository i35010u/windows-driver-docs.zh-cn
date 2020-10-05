---
title: Windows 8 中的 DirectX 功能改进
description: Windows 8 包含 Microsoft DirectX 功能改进，可让开发人员、最终用户和系统制造商受益。
ms.assetid: 0622DA0D-41ED-4B47-B090-8D5B85E10EB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c562cdb8faea8de134821a4b189180be94d606b7
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732881"
---
# <a name="directx-feature-improvements-in-windows-8"></a>Windows 8 中的 DirectX 功能改进


Windows 8 包含 Microsoft DirectX 功能改进，可让开发人员、最终用户和系统制造商受益。

功能改进包括以下几个方面：

-   [像素格式 (5551、565、4444) ](#pixelformats)：更高的能耗硬件配置上的 DirectX 应用程序性能。
-   [双精度着色器功能](#dblshader)：高级着色器模型性能改进，使你能够在 GPU 上执行更多操作而不涉及 CPU。
-   [与目标无关的光栅](#tir)化： Direct2D 应用程序的性能抗锯齿路径更高。
-   [无覆盖和丢弃](#noow)：移动平台上的 Microsoft Direct3D 11.1 应用程序的性能更高，使用基于磁贴的呈现器的电源约束设备上的性能更高。
-   [每个阶段 uav](#uav)：增加了在 DirectX 11.1 硬件上的所有着色器阶段启用着色器调试的功能。
-   [用于支持 Stereoscopic 3d)  (的纹理数组的跨进程共享 ](#stereo)：提供启用 Stereoscopic 三维的基础。
-   [具有多样本抗锯齿示例访问的无序访问视图](#unordered)：允许 Direct3D 11 应用程序实现高质量渲染算法，无需为大量示例分配内存。
-   [逻辑 ops](#logicops)：改进了延迟的底纹技术。
-   [改进了对常量缓冲区的控制](#buffers)：适用于游戏开发人员的高效缓冲区管理。

## <a name="span-idpixelformatsspanspan-idpixelformatsspanpixel-formats-5551-565-4444"></a><span id="pixelformats"></span><span id="PIXELFORMATS"></span>像素格式 (5551、565、4444) 


为了更好地支持使用 DirectX 在低功耗配置中使用图形，Windows 8 的 Direct3D 中必须支持来自 [**DXGI \_ 格式**](/windows/win32/api/dxgiformat/ne-dxgiformat-dxgi_format) 枚举的以下 DirectX 9 像素格式：

-   **DXGI \_ FORMAT \_ B5G6R5 \_ UNORM**
-   **DXGI \_ FORMAT \_ B5G5R5A1 \_ UNORM**
-   **DXGI \_ FORMAT \_ B4G4R4A4 \_ UNORM**

在 DirectX 应用程序中，这些附加格式可提高低功耗硬件的性能。 这些格式在所有 Gpu 上都受支持。 此表描述了对这些格式所需的支持，具体取决于硬件功能级别。

**根据硬件功能级别所需的格式支持**

| 功能                       | 功能级别 9 \_ x                                      | 功能级别10。0                                             | 功能级别10。1                        | 功能级别 11 +                         |
|----------------------------------|---------------------------------------------------------|----------------------------------------------------------------|-------------------------------------------|-------------------------------------------|
| 类型化缓冲区                     | 否                                                      | 必选                                                       | 必选                                  | 必需                                  |
| 输入汇编程序顶点缓冲区    | 否                                                      | 可选                                                       | 可选                                  | 可选                                  |
| Texture1D                        | 否                                                      | 必选                                                       | 必选                                  | 必需                                  |
| Texture2D                        | 必选                                                | 必选                                                       | 必选                                  | 必需                                  |
| Texture3D                        | 否                                                      | 必选                                                       | 必选                                  | 必需                                  |
| TextureCube                      | 必选                                                | 必选                                                       | 必选                                  | 必需                                  |
| 着色器 ld\*                      | 否                                                      | 必选                                                       | 必选                                  | 必需                                  |
| \*带有筛选) 的着色器示例 ( | 必选                                                | 必选                                                       | 必选                                  | 必需                                  |
| 着色器 gather4                   | 否                                                      | 否                                                             | 否                                        | 必须                                  |
| Mipmap                           | 必选                                                | 必选                                                       | 必选                                  | 必需                                  |
| Mipmap 自动生成           | 对于565是必需的，对于4444，为可选，5551               | 对于565是必需的，对于4444，为可选，5551                      | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |
| RenderTarget                     | 对于565是必需的，对于4444，则不是，5551                     | 对于565是必需的，对于4444，为可选，5551                      | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |
| Blendable RenderTarget           | 对于565是必需的，对于4444，则不是，5551                     | 对于565是必需的，对于4444，为可选，5551                      | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |
| UAV 类型存储                  | 否                                                      | 否                                                             | 否                                        | 可选                                  |
| CPU 锁定                     | 必选                                                | 必选                                                       | 必选                                  | 必需                                  |
| 4x MSAA                          | 可选                                                | 可选                                                       | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |
| 8x MSAA                          | 可选                                                | 可选                                                       | 可选                                  | 对于565是必需的，对于4444，为可选，5551 |
| 其他 MSAA 示例计数          | 可选                                                | 可选                                                       | 可选                                  | 可选                                  |
| 多级采样解析              | 如果 MSAA 支持 565) ，则需要 (，4444，5551 | 如果 MSAA 支持 565) ，则必需 (，4444，5551  | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |
| 多级负载                 | 否                                                      | 如果 MSAA 支持 565) ，则必需 (，4444，5551)  | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |

 

## <a name="span-iddblshaderspanspan-iddblshaderspandouble-precision-shader-functionality"></a><span id="dblshader"></span><span id="DBLSHADER"></span>双精度着色器功能


在 Windows 8 中，Windows 显示驱动程序模型 (支持双精度的 WDDM) 1.2 驱动程序还必须支持所有着色器阶段中高级着色器模型5的其他双精度浮点指令。 说明如下：

-   双精度倒数
-   双精度分隔
-   双精度融合的乘法-加法

由于运行时可以将这些指令直接传递给驱动程序，因此实现可以优化其性能，或将其作为专用于硬件的单个说明来实现。

**注意**   若要使用这些功能，开发人员必须确保在 \_ \_ \_ \_ WDDM 1.2 或更高版本的驱动程序上，开发人员的功能级别11或更高版本的功能级别为11或更高 (D3D11 功能双精度) 。

 

### <a name="span-idsum_of_absolute_differencesspanspan-idsum_of_absolute_differencesspanspan-idsum_of_absolute_differencesspansum-of-absolute-differences"></a><span id="Sum_of_absolute_differences"></span><span id="sum_of_absolute_differences"></span><span id="SUM_OF_ABSOLUTE_DIFFERENCES"></span>绝对差异的总和

映像处理是新式设备中的一个关键应用程序。 常见操作是模式匹配或搜索。 视频编码操作通常会搜索匹配的正方形磁贴 (通常为8x8 或 16x16) ，而图像识别算法搜索由位掩码标识的更一般的形状。 为了提高这些方案的性能，在所有着色器阶段中，已将新的内部函数添加到了着色器模型 5.0 (HLSL) 的 Microsoft 高级着色器语言。 此内部 msad4 ( # A1 对应于并生成一组在着色器 IL 中 (MSAD) 说明的绝对差异的掩码。 所有 WDDM 1.2 和更高版本的驱动程序都必须直接在硬件中或作为一组其他说明 (模拟) 来支持此指令。

**注意**   理想情况下，应实现 MSAD 指令，使溢出导致饱和度，而不是换行行为。 请注意，溢出行为是不确定的。

开发人员必须检查以确保在 \_ \_ WDDM 1.2 或更高版本的驱动程序上运行的功能级别为11或更高版本，才能使用此功能。 开发人员不得依赖于溢出的累积值的结果准确性 (也就是说，请在 65535) 之前。

 

## <a name="span-idtirspanspan-idtirspantarget-independent-rasterization-tir"></a><span id="tir"></span><span id="TIR"></span>独立于目标的光栅化 (TIR) 


与目标无关的光栅化 (TIR) 为涉及结构化图形的高质量抗锯齿的 Direct2D 使用方案提供高性能抗锯齿路径。 TIR 使 Direct2D 能够将光栅化步骤从 CPU 移动到 GPU，同时保留 Direct2D 的抗锯齿语义和质量。 使用此功能，软件层可以评估大量的子像素样本位置以供覆盖，但仅分配较少数量的样本所需的内存。 这提供了使用 GPU 呈现的性能优势，但仍保留了 CPU 呈现实现的图像质量。 这允许将单个样本广播到多样本抗锯齿呈现目标的多个示例。

### <a name="span-idsamplecount__1__limited_tir_on_10__101___11_spanspan-idsamplecount__1__limited_tir_on_10__101___11_spanspan-idsamplecount__1__limited_tir_on_10__101___11_spansamplecount-1-limited-tir-on-10-101--11"></a><span id="SampleCount__1__Limited_TIR_on_10__10.1___11_"></span><span id="samplecount__1__limited_tir_on_10__10.1___11_"></span><span id="SAMPLECOUNT__1__LIMITED_TIR_ON_10__10.1___11_"></span>SampleCount = 1 (10.1 TIR & 11 11) 

Direct3D 10.0-Direct3D 11.0 硬件 (和功能级别 10 \_ 0-11 \_ 0) 支持将 ForcedSampleCount 设置为 1 (和呈现目标视图) 的任何样本计数，以及所述的限制 (例如，无深度/模具) 。

对于 10 \_ 0、10 \_ 1 和 11 \_ 0 硬件， [**D3D11 \_ 1 \_ DDI \_ 光栅 \_ **](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1_ddi_rasterizer_desc)化程序 DESC。**ForcedSampleCount** 设置为1，因此，不能将行呈示配置为2三角形 (四边形) 的模式 (也就是说， **MultisampleEnable** 状态不能设置为 true) 。 此限制不适用于11个 \_ 硬件。 请注意， **MultisampleEnable** 状态的命名会产生误导，因为它不再有任何内容可用于启用多级多级操作;相反，它现在是一个控件和 **AntialiasedLineEnable** 的控件，用于选择线条呈现模式。

这种与目标无关的光栅光栅化形式（ **ForcedSampleCount** = 1）与 direct3d 10.0 中提供的模式密切匹配，但对于 direct3d 10.1 和 direct3d (和功能级别为 10 \_ 1 和 11 \_ 0) ，因为 API 发生了更改。 在 Direct3D 10.0 中，此模式是中心取样的渲染，甚至是在 **MultisampleEnable** 设置为 false (时可用 (MSAA) 图面上，可以通过切换 **MultisampleEnable**) 来切换。 在 Direct3D 10.1 + 中， **MultisampleEnable** 不会再影响多级 (（尽管名称) ），并且仅控制行呈现行为。

## <a name="span-idnoowspanspan-idnoowspanno-overwrite-and-discard"></a><span id="noow"></span><span id="NOOW"></span>无覆盖和丢弃


### <a name="span-idrendering_content_on_a_tile-based_deferred-rendering__tbdr__architecturespanspan-idrendering_content_on_a_tile-based_deferred-rendering__tbdr__architecturespanspan-idrendering_content_on_a_tile-based_deferred-rendering__tbdr__architecturespanrendering-content-on-a-tile-based-deferred-rendering-tbdr-architecture"></a><span id="Rendering_content_on_a_tile-based_deferred-rendering__TBDR__architecture"></span><span id="rendering_content_on_a_tile-based_deferred-rendering__tbdr__architecture"></span><span id="RENDERING_CONTENT_ON_A_TILE-BASED_DEFERRED-RENDERING__TBDR__ARCHITECTURE"></span>基于磁贴的延迟渲染 (TBDR) 体系结构呈现内容

Direct3D 11.1 中的呈现目标现在可以通过使用一组新的资源 Api 来支持放弃行为。 开发人员必须了解这一功能，并再次调用 ( # A1 方法，以便更有效地在 TBDR 体系结构 (上运行，而不会对传统的图形硬件) 造成负面影响。 这将提高移动平台和使用平铺呈现器的其他受电源限制的设备的性能。

### <a name="span-idupdating_resources_on_a_tbdr_architecturespanspan-idupdating_resources_on_a_tbdr_architecturespanspan-idupdating_resources_on_a_tbdr_architecturespanupdating-resources-on-a-tbdr-architecture"></a><span id="Updating_resources_on_a_TBDR_architecture"></span><span id="updating_resources_on_a_tbdr_architecture"></span><span id="UPDATING_RESOURCES_ON_A_TBDR_ARCHITECTURE"></span>在 TBDR 体系结构上更新资源

由于 TBDR 体系结构在相同的命令缓冲区上完成多次传递，因此，在上一次绘图调用过程中未修改子资源的一部分时，必须特别小心通知驱动程序。 \_在 Direct3D**UpdateSubResource**函数上进行 "无覆盖" 使用有助于驱动程序管理未对纹理区域进行上一次绘图调用的资源。 这只要求你将应用程序的意图通知驱动程序放弃现有数据，或防止其被覆盖。 这可以在 TBDR 体系结构上实现更高效的呈现，并在传统桌面硬件上运行时不会产生处罚。

Direct3D 11 UpdateSubresource ( # A1 和 CopySubresourceRegions Api 的新变体，它们都更新了 GPU 图面的一部分，提供了不能在其中 \_ 指定覆盖或放弃的 "添加标志" 字段。

这些 Api 会将 Direct3D 11.1 设备驱动程序接口驱动 (DDI) 和 Direct3D 9 DDIs。 需要为任何 DirectX 9 + 硬件使用新的驱动程序来支持修改后的 BLT、BUFBLT、VOLBLT 和 TEXBLT DDIs，方法是添加此处所述的标志。

对于包含 Direct3D 11.1 驱动程序的所有 Direct3D 10 + 硬件，也需要支持这些。

## <a name="span-iduavspanspan-iduavspanuavs-at-every-stage"></a><span id="uav"></span><span id="UAV"></span>每个阶段的 Uav


在 Microsoft Direct3D 11 中，Uav) 的无序访问 (视图数在计算着色器上被限制为八个，并在像素着色器 (RTVs) + Uav) 到8个组合 (呈现目标视图。 在 DirectX 11.1 中，可以绑定的数已增加。 对于 DirectCompute，此限制现在为64，而对于图形，输出合并上的合并合计限制为 64 (也就是说，图形可以有64减去 RTVs) 可能使用的最多8个。

无序访问视图可以从任何着色器阶段访问，但仍会从图形管道的总数中排除

在每个着色器阶段添加 Uav 可将调试信息添加到管道。 这种轻松开发使 Windows 成为编写 GPU 加速应用程序的更理想平台。

这需要至少一个 DirectX 11.1 功能级别。

## <a name="span-idstereospanspan-idstereospancross-process-sharing-of-texture-arrays-for-supporting-stereoscopic-3-d"></a><span id="stereo"></span><span id="STEREO"></span>用于支持 Stereoscopic 3-d 的纹理数组 (的跨进程共享) 


尽管 Stereoscopic 3-d 是一项可选的 WDDM 1.2 系统功能，但所有 WDDM 1.2 设备驱动程序都必须实现基础结构，无论它们是否支持 Stereoscopic 3-d 系统功能。

DirectX 10 (或更高) 功能的图形硬件必须支持纹理阵列的跨进程共享。 此功能提供启用 Stereoscopic 3-d 的基础。 WDDM 1.2 Direct3D DDIs 需要支持遍布缓冲区，因为呈现目标独立于硬件功能级别。

此要求可确保立体声应用程序不会在 mono 模式下出现故障。 例如：即使对于系统上未启用立体声的情况，应用程序也应该能够创建立体声交换链或遍布缓冲器作为渲染目标，然后调用 " **现有**"。 在这种情况下，只 (中显示左视图，或者如果设置了*首选*的   Microsoft DirectX 图形基础结构 (DXGI) 存在标志，则只) 右视图。

因此，WDDM 1.2 驱动程序 (完整的图形 & 呈现设备) 必须支持 Direct3D 11 Api，方法是为纹理数组添加跨进程共享支持。 在早期版本中，跨进程共享资源只能是单层图面。 在 Windows 8 中，共享阵列的最大大小是 (的两个元素，这些元素对于立体声) 来说已经足够了。 有关此要求的详细信息，请参阅 **¦ Stereoscopic3DArraySupport** In [Windows 硬件认证要求](/previous-versions/windows/hardware/cert-program/)。 其他相关的 Microsoft WindowsWindowsWindows HCK 要求是 **¦ ProcessingStereoscopicVideoContent** 和 **Stereoscopic3DModes**。

## <a name="span-idunorderedspanspan-idunorderedspanuavs-with-multi-sample-anti-alias-sample-access"></a><span id="unordered"></span><span id="UNORDERED"></span>具有多样本抗锯齿示例访问的 Uav


Direct3D 11 允许光栅化访问视图 (Uav) ，无 (RTVs) /DSVs 绑定的呈现目标视图。 即使 Uav 可以具有任意大小，实现也可以使用视区/剪刀矩形的像素尺寸来操作光栅化程序。 DirectX 11 硬件的示例模式仅为单个样本。 DirectX 11.1 硬件规范展开以允许多个示例。 这是与目标无关的光栅化的变体，其中只绑定了 Uav 的输出。

UAV-现在可以通过将 ForcedSampleCount 状态合在一起，在光栅化程序上使用多级进行呈现，并且示例模式限制为0、1、4和 8 (不是16，TIR 支持) 。  (在分配方面，Uav 本身并不多采样。 ) 设置为0等效于设置 1-单示例光栅化。

着色器可以请求具有仅限 UAV 呈现的像素频率调用。 但是，请求的采样频率调用无效 () 生成未定义的底纹结果。 SampleMask 光栅化状态根本不会影响光栅化行为。

在 DirectX 11.0 + 硬件上提供对此功能的支持，包括不支持 \_ 具有 RTVs 的第11个目标独立光栅的硬件。 该驱动程序可以报告它是否支持 UAV 的多样本抗锯齿 (访问) 呈现， (表示4和8示例都支持) 。 所有 DirectX 11 + 硬件支持1。 如果硬件可以通过 RTVs 运行完整的 11 \_ 个与目标无关的光栅化 (这需要) 支持16个示例，则)  (需要仅支持 UAV 的 MSAA 光栅

此功能使应用程序能够实现高质量渲染算法，如分析抗锯齿，无需为大量示例分配内存。

## <a name="span-idlogicopsspanspan-idlogicopsspanlogic-operations"></a><span id="logicops"></span><span id="LOGICOPS"></span>逻辑操作


如果允许在输出合并时进行逻辑操作，则可以对当前无法执行的映像执行一些操作。 例如，可以更有效、更轻松地计算掩码，还可以为三维渲染实现新式延迟着色技术。

尽管此功能在大多数三维硬件中存在，但目前并不像颜色混合那样通用。 因此，逻辑操作的配置在以下方面受到限制：

-   当在第一个 RT blend desc 中使用逻辑操作数时，IndependentBlendEnable 必须设置为 false，以便将相同的逻辑 op 应用于所有 RTs。
-   使用逻辑操作数时，所有 RenderTargets 绑定的格式必须为 UINT 或圣马丁，否则呈现是不确定的。

## <a name="span-idbuffersspanspan-idbuffersspanimproved-control-of-constant-buffers"></a><span id="buffers"></span><span id="BUFFERS"></span>更好地控制常量缓冲区


### <a name="span-idpartialbufferspanspan-idpartialbufferspanpartial-constant-buffer-updates"></a><span id="partialbuffer"></span><span id="PARTIALBUFFER"></span>部分常量缓冲区更新

现在，常量缓冲区需要在寄存器整个缓冲区的更新过程中从源到目标的单一副本。 如果只需要更新常量缓冲区的一部分，则写入的偏移量是理想的。 游戏开发人员需要这种随机访问常量缓冲区的功能，并使常量缓冲区管理更自然、更有效。 这些功能已支持其他缓冲区类型，并已添加到 WDDM 1.2 驱动程序中的常量缓冲区。

对于包含 Direct3D 11.1 驱动程序的所有 Direct3D 10 + 硬件，必须支持此功能。 对于开发人员来说，这会在 DirectX 9 硬件上模拟，使其适用于所有功能级别。

**注意**   你必须指定 "不 \_ 覆盖" 或 "丢弃" 标志。

 

### <a name="span-idoffsetting_constant_buffer_updatesspanspan-idoffsetting_constant_buffer_updatesspanspan-idoffsetting_constant_buffer_updatesspanoffsetting-constant-buffer-updates"></a><span id="Offsetting_constant_buffer_updates"></span><span id="offsetting_constant_buffer_updates"></span><span id="OFFSETTING_CONSTANT_BUFFER_UPDATES"></span>偏移常量缓冲区更新

高性能游戏引擎的一个常见要求是，收集大量恒定的常量缓冲区更新，使其能够通过单独的**Draw \\ *** 调用进行引用，每个常量都需要自己的常量，同时全部都是。 这可以通过以下方式来实现：允许应用程序创建一个较大的缓冲区，然后将各个着色器指向其内部的区域 (类似于视图，但不需要创建整个对象来描述视图) 。

现在可以创建大容量缓冲区，其大小大于单个着色器可寻址的最大常量缓冲区大小 (最多 4096 16 个字节的元素-65kB，其中每个元素均为 1 4-分量着色器常量) 。 现在，常量缓冲区资源大小仅受系统能够处理的内存分配的大小限制。

当使用** \* SetShaderConstants**Api （如**VSSetShaderConstants**）将大于4096的常量缓冲区绑定到管道时，它将显示在着色器中，就像它只是大小为4096个元素一样。

** \* SetShaderConstants**api （ ** \* SetShaderConstants1**）的变体允许将 "FirstConstant" 和 "ConstantCount" 与绑定一起指定。 当着色器以这种方式访问绑定的常量缓冲区时，它看起来就像是以指定的 "FirstConstant" 偏移量开头 (其中，1表示16个字节) 并且大小由 ConstantCount (数量的16字节常量) 定义。 这基本上是较大的常量缓冲区区域的轻型 "视图"。 FirstConstant 和 ConstantCount (都必须是 16) 的倍数。

Direct3D 10 + 硬件的所有 WDDM 1.2 驱动程序必须支持此功能。 Direct3D 11 运行时为功能级别 9 x 模拟适当的行为 \_ 。

## <a name="span-idclearviewspanspan-idclearviewspanclearview"></a><span id="clearview"></span><span id="CLEARVIEW"></span>Clearview


此功能使实现可以对视频内存资源执行高效的清除操作，并在单个 API/DDI 调用中清除多个 rect。 API 包括对定义要清除的资源子集的矩形的支持。 此功能在 DirectX 9 DDI 中受支持，并且对于 Windows 8 驱动程序 (WDDM 1.2) 是必需的。 此方法可提高二维操作的性能，例如，在图像处理和 UI 中使用的操作。

## <a name="span-idcpyflagspanspan-idcpyflagspantileable-copy-flag"></a><span id="cpyflag"></span><span id="CPYFLAG"></span>Tileable 复制标志


Tileable copy 操作允许应用程序通知实现：图像源和目标是像素对齐的，并且不会在后续呈现传递中参与跨像素的信息交换。 这样，在复制操作过程中，通过缓存映像数据的子集，可以显著提高性能。 此功能在 DirectX 9 DDI 中受支持，在 (WDDM 1.2) 的 Windows 8 及更高版本驱动程序中是必需的。

## <a name="span-idblitsspanspan-idblitsspansame-surface-blits"></a><span id="blits"></span><span id="BLITS"></span>相同 surface blits


许多 UI 操作（如滚动）都需要将图像数据从图像的一个部分传输到另一个部分。 此功能添加了对源矩形和目标矩形都在同一图像或资源中的复制操作的支持。 如果源和目标矩形重叠，则实现和驱动程序必须正确地处理这种情况。 DirectX 9 DDI 已经需要此操作，并且所有硬件在 WDDM 1.2 中是必需的。 此方法将显著提高关键 UI 方案的性能。

## <a name="span-iddirect3d_111_ddispanspan-iddirect3d_111_ddispandirect3d-111-ddi"></a><span id="direct3d_11.1_ddi"></span><span id="DIRECT3D_11.1_DDI"></span>Direct3D 11.1 DDI


这些函数和结构是适用于 Windows 8 的新功能或更新的：

-   [*AssignDebugBinary*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_assigndebugbinary)
-   [*CalcPrivateBlendStateSize (D3D11 \_ 1) *](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivateblendstatesize)
-   [*ClearView*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_clearview)
-   [*DefaultConstantBufferUpdateSubresourceUP (D3D11 \_ 1) *](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_resourceupdatesubresourceup)
-   [*ResourceUpdateSubresourceUP (D3D11 \_ 1) *](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_resourceupdatesubresourceup)
-   [*VsSetConstantBuffers (D3D11 \_ 1) *](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_setconstantbuffers)
-   [**D3D11 \_ 1DDI \_ D3D11 \_ OPTIONS \_ 数据**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_d3d11_options_data)
-   [**D3DDDI \_ BLTFLAGS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_bltflags)
-   [**D3DDDI \_ 复制 \_ 标志**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_copy_flags)
-   [**D3DDDIARG \_ BUFFERBLT1**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_bufferblt1)
-   [**D3DDDIARG \_ 放弃**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_discard)
-   [**D3DDDIARG \_ TEXBLT1**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_texblt1)
-   [**D3DDDIARG \_ VOLUMEBLT1**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_volumeblt1)
-   [**D3DDDICAPS \_ 体系结构 \_ 信息**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicaps_architecture_info)
-   [**D3DDDICAPS \_ 着色器 \_ 最小 \_ 精度**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddicaps_shader_min_precision)
-   [**D3DDDICAPS \_ 着色器 \_ 最小 \_ 精度 \_ 支持**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicaps_shader_min_precision_support)
-   [**D3DDDICAPS \_ 类型**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)

