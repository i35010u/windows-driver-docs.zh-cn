---
title: Windows 8 中的 DirectX 功能改进
description: Windows 8 包含 Microsoft DirectX 功能改进，可让开发人员、最终用户和系统制造商受益。
ms.assetid: 0622DA0D-41ED-4B47-B090-8D5B85E10EB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb1df9f714d02b0f85941cb068ac746904c83195
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838998"
---
# <a name="directx-feature-improvements-in-windows-8"></a>Windows 8 中的 DirectX 功能改进


Windows 8 包含 Microsoft DirectX 功能改进，可让开发人员、最终用户和系统制造商受益。

功能改进包括以下几个方面：

-   [像素格式（5551，565，4444）](#pixelformats)：更高能耗硬件配置上的 DirectX 应用程序的性能。
-   [双精度着色器功能](#dblshader)：高级着色器模型性能改进，使你能够在 GPU 上执行更多操作而不涉及 CPU。
-   [与目标无关的光栅](#tir)化： Direct2D 应用程序的性能抗锯齿路径更高。
-   [无覆盖和丢弃](#noow)：移动平台上的 Microsoft Direct3D 11.1 应用程序的性能更高，使用基于磁贴的呈现器的电源约束设备上的性能更高。
-   [每个阶段 uav](#uav)：增加了在 DirectX 11.1 硬件上的所有着色器阶段启用着色器调试的功能。
-   [纹理数组的跨进程共享（用于支持 Stereoscopic 3d）](#stereo)：提供启用 Stereoscopic 三维的基础。
-   [具有多样本抗锯齿示例访问的无序访问视图](#unordered)：允许 Direct3D 11 应用程序实现高质量渲染算法，无需为大量示例分配内存。
-   [逻辑 ops](#logicops)：改进了延迟的底纹技术。
-   [改进了对常量缓冲区的控制](#buffers)：适用于游戏开发人员的高效缓冲区管理。

## <a name="span-idpixelformatsspanspan-idpixelformatsspanpixel-formats-5551-565-4444"></a><span id="pixelformats"></span><span id="PIXELFORMATS"></span>像素格式（5551，565，4444）


为了更好地支持使用 DirectX 在低功耗配置中使用图形，Windows 8 的 Direct3D 中必须支持以下基于[**DXGI\_格式**](https://docs.microsoft.com/windows/desktop/api/dxgiformat/ne-dxgiformat-dxgi_format)枚举的 DirectX 9 像素格式：

-   **DXGI\_格式\_B5G6R5\_UNORM**
-   **DXGI\_格式\_B5G5R5A1\_UNORM**
-   **DXGI\_格式\_B4G4R4A4\_UNORM**

在 DirectX 应用程序中，这些附加格式可提高低功耗硬件的性能。 这些格式在所有 Gpu 上都受支持。 此表描述了对这些格式所需的支持，具体取决于硬件功能级别。

**根据硬件功能级别所需的格式支持**

| 功能                       | 功能级别 9\_x                                      | 功能级别10。0                                             | 功能级别10。1                        | 功能级别 11 +                         |
|----------------------------------|---------------------------------------------------------|----------------------------------------------------------------|-------------------------------------------|-------------------------------------------|
| 类型化缓冲区                     | 无                                                      | 必需                                                       | 必需                                  | 必需                                  |
| 输入汇编程序顶点缓冲区    | 无                                                      | 可选                                                       | 可选                                  | 可选                                  |
| Texture1D                        | 无                                                      | 必需                                                       | 必需                                  | 必需                                  |
| Texture2D                        | 必需                                                | 必需                                                       | 必需                                  | 必需                                  |
| Texture3D                        | 无                                                      | 必需                                                       | 必需                                  | 必需                                  |
| TextureCube                      | 必需                                                | 必需                                                       | 必需                                  | 必需                                  |
| 着色器 ld\*                      | 无                                                      | 必需                                                       | 必需                                  | 必需                                  |
| 着色器示例\* （带有筛选） | 必需                                                | 必需                                                       | 必需                                  | 必需                                  |
| 着色器 gather4                   | 无                                                      | 无                                                             | 无                                        | 必需                                  |
| Mipmap                           | 必需                                                | 必需                                                       | 必需                                  | 必需                                  |
| Mipmap 自动生成           | 对于565是必需的，对于4444，为可选，5551               | 对于565是必需的，对于4444，为可选，5551                      | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |
| RenderTarget                     | 对于565是必需的，对于4444，则不是，5551                     | 对于565是必需的，对于4444，为可选，5551                      | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |
| Blendable RenderTarget           | 对于565是必需的，对于4444，则不是，5551                     | 对于565是必需的，对于4444，为可选，5551                      | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |
| UAV 类型存储                  | 无                                                      | 无                                                             | 无                                        | 可选                                  |
| CPU 锁定                     | 必需                                                | 必需                                                       | 必需                                  | 必需                                  |
| 4x MSAA                          | 可选                                                | 可选                                                       | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |
| 8x MSAA                          | 可选                                                | 可选                                                       | 可选                                  | 对于565是必需的，对于4444，为可选，5551 |
| 其他 MSAA 示例计数          | 可选                                                | 可选                                                       | 可选                                  | 可选                                  |
| 多级采样解析              | 必需（如果支持 MSAA）对于565，no = 4444，5551 | 必需（如果支持 MSAA） 5551 4444，565  | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |
| 多级负载                 | 无                                                      | 必需（如果支持 MSAA）565，对于 4444 5551，则为可选 | 对于565是必需的，对于4444，为可选，5551 | 对于565是必需的，对于4444，为可选，5551 |

 

## <a name="span-iddblshaderspanspan-iddblshaderspandouble-precision-shader-functionality"></a><span id="dblshader"></span><span id="DBLSHADER"></span>双精度着色器功能


在 Windows 8 中，支持双精度的 Windows 显示驱动程序模型（WDDM）1.2 驱动程序还必须支持所有着色器阶段中高级着色器模型5的其他双精度浮点指令。 说明如下：

-   双精度倒数
-   双精度分隔
-   双精度融合的乘法-加法

由于运行时可以将这些指令直接传递给驱动程序，因此实现可以优化其性能，或将其作为专用于硬件的单个说明来实现。

**请注意**   要使用这些功能，开发人员必须确保在 WDDM 1.2 或更高版本的驱动程序上，它们使用\_级别\_11 或更高版本的功能（D3D11\_功能\_双精度型）运行。

 

### <a name="span-idsum_of_absolute_differencesspanspan-idsum_of_absolute_differencesspanspan-idsum_of_absolute_differencesspansum-of-absolute-differences"></a><span id="Sum_of_absolute_differences"></span><span id="sum_of_absolute_differences"></span><span id="SUM_OF_ABSOLUTE_DIFFERENCES"></span>绝对差异的总和

映像处理是新式设备中的一个关键应用程序。 常见操作是模式匹配或搜索。 视频编码操作通常会搜索匹配的正方形磁贴（通常为8x8 或16x16），而图像识别算法会搜索由位掩码标识的更一般的形状。 为了提高这些方案的性能，所有着色器阶段的着色器模型5.0 的 Microsoft 高级着色器语言（HLSL）中添加了一个新的内部函数。 此内部 msad4 （）对应于并在着色器 IL 中生成一组绝对差异（MSAD）指令。 所有 WDDM 1.2 和更高版本的驱动程序都必须直接在硬件中或作为一组其他说明（模拟）支持此指令。

**请注意**   理想情况下，应实现 MSAD 指令，使溢出导致饱和度，而不是换行行为。 请注意，溢出行为是不确定的。

开发人员必须检查以确保在 WDDM 1.2 或更高版本的驱动程序上使用功能\_级别\_11 或更高版本运行，才能使用此功能。 开发人员不得依赖于溢出值（即在65535以上）的结果准确性。

 

## <a name="span-idtirspanspan-idtirspantarget-independent-rasterization-tir"></a><span id="tir"></span><span id="TIR"></span>独立于目标的光栅化（TIR）


与目标无关的光栅化（TIR）为涉及结构化图形的高质量抗锯齿的 Direct2D 使用方案提供高性能抗锯齿路径。 TIR 使 Direct2D 能够将光栅化步骤从 CPU 移动到 GPU，同时保留 Direct2D 的抗锯齿语义和质量。 使用此功能，软件层可以评估大量的子像素样本位置以供覆盖，但仅分配较少数量的样本所需的内存。 这提供了使用 GPU 呈现的性能优势，但仍保留了 CPU 呈现实现的图像质量。 这允许将单个样本广播到多样本抗锯齿呈现目标的多个示例。

### <a name="span-idsamplecount__1__limited_tir_on_10__101___11_spanspan-idsamplecount__1__limited_tir_on_10__101___11_spanspan-idsamplecount__1__limited_tir_on_10__101___11_spansamplecount-1-limited-tir-on-10-101--11"></a><span id="SampleCount__1__Limited_TIR_on_10__10.1___11_"></span><span id="samplecount__1__limited_tir_on_10__10.1___11_"></span><span id="SAMPLECOUNT__1__LIMITED_TIR_ON_10__10.1___11_"></span>SampleCount = 1 （限制为 TIR & 10，10.1 11）

Direct3D 10.0-Direct3D 11.0 硬件（和功能级别 10\_0-11\_0）支持将 ForcedSampleCount 设置为1（以及呈现器目标视图的任何样本计数）以及所述的限制（例如，无深度/模具）。

对于 10\_0、10\_1 和 11\_0 硬件，当[**D3D11\_1\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1_ddi_rasterizer_desc)**ForcedSampleCount**设置为1，因此，不能将行渲染配置为基于2三角形（四边形）的模式（即，不能将**MultisampleEnable**状态设置为 "true"）。 此限制对于11个\_1 硬件不存在。 请注意， **MultisampleEnable**状态的命名会产生误导，因为它不再有任何内容可用于启用多级多级操作;相反，它现在是一个控件和**AntialiasedLineEnable**的控件，用于选择线条呈现模式。

这种与目标无关的光栅光栅化形式（ **ForcedSampleCount** = 1）与 direct3d 10.0 中提供的模式密切匹配，但在 direct3d 10.1 和 Direct3D 中变得不可用（和功能级别 10\_1 和 11\_0）。更改为 API。 在 Direct3D 10.0 中，此模式是中心取样的渲染，甚至是在**MultisampleEnable**设置为 false 时提供的多个样本抗锯齿（MSAA）图面上（可以通过切换**MultisampleEnable**来切换）。 在 Direct3D 10.1 + 中， **MultisampleEnable**不再影响多级（尽管名称），并且仅控制行呈现行为。

## <a name="span-idnoowspanspan-idnoowspanno-overwrite-and-discard"></a><span id="noow"></span><span id="NOOW"></span>无覆盖和丢弃


### <a name="span-idrendering_content_on_a_tile-based_deferred-rendering__tbdr__architecturespanspan-idrendering_content_on_a_tile-based_deferred-rendering__tbdr__architecturespanspan-idrendering_content_on_a_tile-based_deferred-rendering__tbdr__architecturespanrendering-content-on-a-tile-based-deferred-rendering-tbdr-architecture"></a><span id="Rendering_content_on_a_tile-based_deferred-rendering__TBDR__architecture"></span><span id="rendering_content_on_a_tile-based_deferred-rendering__tbdr__architecture"></span><span id="RENDERING_CONTENT_ON_A_TILE-BASED_DEFERRED-RENDERING__TBDR__ARCHITECTURE"></span>基于磁贴的延迟渲染（TBDR）体系结构呈现内容

Direct3D 11.1 中的呈现目标现在可以通过使用一组新的资源 Api 来支持放弃行为。 开发人员必须了解此功能，并调用其他放弃（）方法以更有效地在 TBDR 体系结构上运行（对传统的图形硬件没有负面影响）。 这将提高移动平台和使用平铺呈现器的其他受电源限制的设备的性能。

### <a name="span-idupdating_resources_on_a_tbdr_architecturespanspan-idupdating_resources_on_a_tbdr_architecturespanspan-idupdating_resources_on_a_tbdr_architecturespanupdating-resources-on-a-tbdr-architecture"></a><span id="Updating_resources_on_a_TBDR_architecture"></span><span id="updating_resources_on_a_tbdr_architecture"></span><span id="UPDATING_RESOURCES_ON_A_TBDR_ARCHITECTURE"></span>在 TBDR 体系结构上更新资源

由于 TBDR 体系结构在相同的命令缓冲区上完成多次传递，因此，在上一次绘图调用过程中未修改子资源的一部分时，必须特别小心通知驱动程序。 在 Direct3D**UpdateSubResource**函数上使用 "无\_覆盖使用情况" 有助于驱动程序管理未对纹理区域进行上一次绘图调用的资源。 这只要求你将应用程序的意图通知驱动程序放弃现有数据，或防止其被覆盖。 这可以在 TBDR 体系结构上实现更高效的呈现，并在传统桌面硬件上运行时不会产生处罚。

Direct3D 11 UpdateSubresource （）和 CopySubresourceRegions Api 的新变体，它们都更新了 GPU 图面的一部分，提供了不能指定\_覆盖或放弃的 "添加标志" 字段。

这些 Api 驱动 Direct3D 11.1 设备驱动程序接口（DDI）和 Direct3D 9 DDIs。 需要为任何 DirectX 9 + 硬件使用新的驱动程序来支持修改后的 BLT、BUFBLT、VOLBLT 和 TEXBLT DDIs，方法是添加此处所述的标志。

对于包含 Direct3D 11.1 驱动程序的所有 Direct3D 10 + 硬件，也需要支持这些。

## <a name="span-iduavspanspan-iduavspanuavs-at-every-stage"></a><span id="uav"></span><span id="UAV"></span>每个阶段的 Uav


在 Microsoft Direct3D 11 中，无序访问视图（Uav）的数量在计算着色器中限制为8，而在像素着色器上限制为8组合（呈现目标视图（RTVs） + Uav）。 在 DirectX 11.1 中，可以绑定的数已增加。 对于 DirectCompute，此限制现在为64，而对于图形，输出合并到输出合并的总限制为64（也就是说，图形可以有64减去 RTVs 可能使用的最多8个）。

无序访问视图可以从任何着色器阶段访问，但仍会从图形管道的总数中排除

在每个着色器阶段添加 Uav 可将调试信息添加到管道。 这种轻松开发使 Windows 成为编写 GPU 加速应用程序的更理想平台。

这需要至少一个 DirectX 11.1 功能级别。

## <a name="span-idstereospanspan-idstereospancross-process-sharing-of-texture-arrays-for-supporting-stereoscopic-3-d"></a><span id="stereo"></span><span id="STEREO"></span>纹理数组的跨进程共享（用于支持 Stereoscopic 3-d）


尽管 Stereoscopic 3-d 是一项可选的 WDDM 1.2 系统功能，但所有 WDDM 1.2 设备驱动程序都必须实现基础结构，无论它们是否支持 Stereoscopic 3-d 系统功能。

支持 DirectX 10 （或更高版本）的图形硬件必须支持纹理阵列的跨进程共享。 此功能提供启用 Stereoscopic 3-d 的基础。 WDDM 1.2 Direct3D DDIs 需要支持遍布缓冲区，因为呈现目标独立于硬件功能级别。

此要求可确保立体声应用程序不会在 mono 模式下出现故障。 例如：即使对于系统上未启用立体声的情况，应用程序也应该能够创建立体声交换链或遍布缓冲器作为渲染目标，然后调用 "**现有**"。 在这种情况下，只会显示左侧视图（或者，如果已设置 *首选*的 "Microsoft DirectX 图形基础结构（DXGI）" 标志，则仅显示右侧视图）。

因此，WDDM 1.2 驱动程序（完整图形 & 渲染设备）必须支持 Direct3D 11 Api，方法是为纹理数组添加跨进程共享支持。 在早期版本中，跨进程共享资源只能是单层图面。 在 Windows 8 中，共享阵列的最大大小是两个元素（对于立体声来说就足够了）。 有关此要求的详细信息，请参阅**¦ Stereoscopic3DArraySupport** In [Windows 硬件认证要求](https://go.microsoft.com/fwlink/p/?linkid=324537)。 其他相关的 Microsoft WindowsWindowsWindows HCK 要求是**¦ ProcessingStereoscopicVideoContent**和**Stereoscopic3DModes**。

## <a name="span-idunorderedspanspan-idunorderedspanuavs-with-multi-sample-anti-alias-sample-access"></a><span id="unordered"></span><span id="UNORDERED"></span>具有多样本抗锯齿示例访问的 Uav


Direct3D 11 允许光栅化访问视图（Uav），但未绑定任何呈现器目标视图（RTVs）。 即使 Uav 可以具有任意大小，实现也可以使用视区/剪刀矩形的像素尺寸来操作光栅化程序。 DirectX 11 硬件的示例模式仅为单个样本。 DirectX 11.1 硬件规范展开以允许多个示例。 这是与目标无关的光栅化的变体，其中只绑定了 Uav 的输出。

UAV-现在可以通过将 ForcedSampleCount 状态合在一起，在光栅化程序上使用多级进行呈现，并且示例模式限制为0、1、4和8（不是 TIR 支持的16）。 （Uav 本身在分配方面并不多采样。）设置为0等效于设置 1-单示例光栅化。

着色器可以请求具有仅限 UAV 呈现的像素频率调用。 但是，请求的采样频率调用无效（产生未定义的底纹结果）。 SampleMask 光栅化状态根本不会影响光栅化行为。

在 DirectX 11.0 + 硬件上提供对此功能的支持，其中包括不支持具有 RTVs 的、与目标无关的第\_11 个级别的的硬件。 该驱动程序可以报告它是否支持 UAV 的多样本反别名示例访问（MSAA）呈现（表示同时支持4和8个示例）。 所有 DirectX 11 + 硬件支持1。 如果硬件可以通过 RTVs （需要16示例支持）来执行 11\_1 与目标无关的光栅化，则需要仅 UAV MSAA 光栅化支持（这意味着仅限 UAV 的情况下为4和8个样本）。

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

**请注意**   必须指定 "不\_覆盖" 或 "丢弃" 标志。

 

### <a name="span-idoffsetting_constant_buffer_updatesspanspan-idoffsetting_constant_buffer_updatesspanspan-idoffsetting_constant_buffer_updatesspanoffsetting-constant-buffer-updates"></a><span id="Offsetting_constant_buffer_updates"></span><span id="offsetting_constant_buffer_updates"></span><span id="OFFSETTING_CONSTANT_BUFFER_UPDATES"></span>偏移常量缓冲区更新

高性能游戏引擎的一个常见要求是，收集大量恒定的常量缓冲区更新，以供单独的**绘图\\** * 调用引用，每个调用都需要自己的常量，同时全部都需要。 这是通过允许应用程序创建一个较大的缓冲区，然后将各个着色器指向其中的区域（类似于视图，但不需要创建整个对象来描述视图）来实现的。

现在可以创建大小大于单个着色器（最多 4096 16 个字节的元素-65kB，其中每个元素均为 1 4-component 着色器常量）的最大常量缓冲区大小的常量缓冲区。 现在，常量缓冲区资源大小仅受系统能够处理的内存分配的大小限制。

当使用 **\*SetShaderConstants**api （例如**VSSetShaderConstants**）将大于4096的常量缓冲区绑定到管道时，它将显示在着色器中，就好像它只是大小为4096个元素一样。

**\*SetShaderConstants**Api **\*SetShaderConstants1**的变体允许将 "FirstConstant" 和 "ConstantCount" 与绑定一起指定。 当着色器以这种方式访问绑定的常量缓冲区时，它看起来就像是以指定的 "FirstConstant" 偏移量（1表示16个字节）开头，并且具有由 ConstantCount 定义的大小（16字节常量的数目）。 这基本上是较大的常量缓冲区区域的轻型 "视图"。 （FirstConstant 和 ConstantCount 必须是16的倍数）。

Direct3D 10 + 硬件的所有 WDDM 1.2 驱动程序必须支持此功能。 Direct3D 11 运行时为功能级别 9\_x 模拟适当的行为。

## <a name="span-idclearviewspanspan-idclearviewspanclearview"></a><span id="clearview"></span><span id="CLEARVIEW"></span>Clearview


此功能使实现可以对视频内存资源执行高效的清除操作，并在单个 API/DDI 调用中清除多个 rect。 API 包括对定义要清除的资源子集的矩形的支持。 此功能在 DirectX 9 DDI 中受支持，Windows 8 驱动程序（WDDM 1.2）需要此功能。 此方法可提高二维操作的性能，例如，在图像处理和 UI 中使用的操作。

## <a name="span-idcpyflagspanspan-idcpyflagspantileable-copy-flag"></a><span id="cpyflag"></span><span id="CPYFLAG"></span>Tileable 复制标志


Tileable copy 操作允许应用程序通知实现：图像源和目标是像素对齐的，并且不会在后续呈现传递中参与跨像素的信息交换。 这样，在复制操作过程中，通过缓存映像数据的子集，可以显著提高性能。 此功能在 DirectX 9 DDI 中受支持，适用于 Windows 8 及更高版本的驱动程序（WDDM 1.2）。

## <a name="span-idblitsspanspan-idblitsspansame-surface-blits"></a><span id="blits"></span><span id="BLITS"></span>相同 surface blits


许多 UI 操作（如滚动）都需要将图像数据从图像的一个部分传输到另一个部分。 此功能添加了对源矩形和目标矩形都在同一图像或资源中的复制操作的支持。 如果源和目标矩形重叠，则实现和驱动程序必须正确地处理这种情况。 DirectX 9 DDI 已经需要此操作，并且所有硬件在 WDDM 1.2 中是必需的。 此方法将显著提高关键 UI 方案的性能。

## <a name="span-iddirect3d_111_ddispanspan-iddirect3d_111_ddispandirect3d-111-ddi"></a><span id="direct3d_11.1_ddi"></span><span id="DIRECT3D_11.1_DDI"></span>Direct3D 11.1 DDI


这些函数和结构是适用于 Windows 8 的新功能或更新的：

-   [*AssignDebugBinary*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_assigndebugbinary)
-   [*CalcPrivateBlendStateSize （D3D11\_1）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivateblendstatesize)
-   [*ClearView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_clearview)
-   [*DefaultConstantBufferUpdateSubresourceUP （D3D11\_1）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_resourceupdatesubresourceup)
-   [*ResourceUpdateSubresourceUP （D3D11\_1）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_resourceupdatesubresourceup)
-   [*VsSetConstantBuffers （D3D11\_1）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_setconstantbuffers)
-   [**D3D11\_1DDI\_D3D11\_选项\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_d3d11_options_data)
-   [**D3DDDI\_BLTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_bltflags)
-   [**D3DDDI\_复制\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_copy_flags)
-   [**D3DDDIARG\_BUFFERBLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_bufferblt1)
-   [**D3DDDIARG\_放弃**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_discard)
-   [**D3DDDIARG\_TEXBLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_texblt1)
-   [**D3DDDIARG\_VOLUMEBLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_volumeblt1)
-   [**D3DDDICAPS\_体系结构\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicaps_architecture_info)
-   [**D3DDDICAPS\_着色器\_MIN\_精度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddicaps_shader_min_precision)
-   [**D3DDDICAPS\_着色器\_MIN\_精度\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicaps_shader_min_precision_support)
-   [**D3DDDICAPS\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)

 

 





