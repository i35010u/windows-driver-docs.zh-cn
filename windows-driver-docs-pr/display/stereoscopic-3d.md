---
title: 立体 3D
description: Windows 8 为 stereoscopic 3-d 方案 (DDI) 平台提供了一致的 API 和设备驱动程序接口，例如游戏和视频播放。
ms.assetid: 2F83E5C6-E333-4BF6-A133-C65A23DAEF62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0afce64884c6b2454a01f4cc133e5bc2626d1d2f
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107210"
---
# <a name="stereoscopic-3d"></a>立体 3D


Windows 8 为 stereoscopic 3-d 方案 (DDI) 平台提供了一致的 API 和设备驱动程序接口，例如游戏和视频播放。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">最小 Windows 显示器驱动程序模型 (WDDM) 版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现-完整图形</td>
<td align="left">可选</td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a> 要求和测试</td>
<td align="left"><p><strong>¦ ProcessingStereoscopicVideoContent</strong></p>
<p><strong>显示 Stereoscopic3DModes</strong></p></td>
</tr>
</tbody>
</table>

 

仅在具有 Stereoscopic 3-d 功能的所有组件的系统上启用 Stereoscopic 3-d 呈现功能。 这些组件包括支持3-d 的显示硬件、图形硬件、外围设备和软件应用程序。 图形堆栈中的立体声设计使所使用的特定可视化或显示技术对操作系统不可知。 显示驱动程序直接与图形显示通信，并通过标准化的扩展显示标识数据 (EDID) 结构来了解显示功能。 仅当驱动程序识别出此类显示器已连接到系统时，驱动程序才枚举立体声功能。

若要在显示器微型端口和用户模式驱动程序中实现立体声功能，请参阅下面的新的或更新的 DDIs 的列表。

"Stereoscopic 显示" 设置是 " **屏幕分辨率** " 控制面板的一部分，如下所示：

![stereoscopic 显示设置](images/stereo3ddisplaysetting.jpg)

" **启用立体声** 设置" 是具有以下状态的复选框：

-   "不可用" (灰显或不可见) ：在不**能使用**立体声显示的系统上显示。
-   设置为 " **已启用** " (选中) ：这是能够在立体声显示器上呈现的系统上的默认设置，表示立体声点播。 默认情况下，桌面窗口管理器 (DWM) 为 mono 模式。 仅当用户 (按需) 启动一个立体声应用时，DWM 才切换为立体声模式。 请注意，在选中此复选框时，DWM 可以为 mono 或立体声模式。
-   设置为 **已禁用** (取消选中) ：如果用户取消选中此设置，则 DWM 处于 mono 模式。 在这种情况下，立体声应用程序以 mono 模式显示。

## <a name="span-idstereoscopic_3-d_kernel-mode_supportspanspan-idstereoscopic_3-d_kernel-mode_supportspanspan-idstereoscopic_3-d_kernel-mode_supportspanstereoscopic-3-d-kernel-mode-support"></a><span id="Stereoscopic_3-D_kernel-mode_support"></span><span id="stereoscopic_3-d_kernel-mode_support"></span><span id="STEREOSCOPIC_3-D_KERNEL-MODE_SUPPORT"></span>Stereoscopic 3-d 内核模式支持


这些 DDIs 更新为 Windows 8，以支持在 VidPN 上 stereoscopic 三维渲染。

-   [**D3D11DDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)
-   [**D3DDDI \_ ALLOCATIONINFO**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)
-   [**D3DKMDT \_ VIDPN \_ 源 \_ 模式 \_ 类型**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_source_mode_type)
-   [**D3DKMT \_ PRESENTFLAGS**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_presentflags)
-   [**DXGI \_ DDI \_ ARG \_ 旋转 \_ 资源 \_ 标识**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_rotate_resource_identities)
-   [**DXGK \_ PRESENTFLAGS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentflags)
-   [**DXGK \_ SETVIDPNSOURCEADDRESS \_ 标志**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_setvidpnsourceaddress_flags)
-   [**DXGKARG \_ OPENALLOCATION**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_openallocation)

## <a name="span-idstereoscopic_3-d_swapchain_ddisspanspan-idstereoscopic_3-d_swapchain_ddisspanspan-idstereoscopic_3-d_swapchain_ddisspanstereoscopic-3-d-swapchain-ddis"></a><span id="Stereoscopic_3-D_swapchain_DDIs"></span><span id="stereoscopic_3-d_swapchain_ddis"></span><span id="STEREOSCOPIC_3-D_SWAPCHAIN_DDIS"></span>Stereoscopic 3-d 存在 DDIs


这些 DDIs 是适用于 Windows 8 的新的或更新的，以支持 stereoscopic 3-d 交换链。

-   [*BltDXGI*](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)
-   [*Blt1DXGI*](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)
-   [*CreateResource (D3D10) *](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)
-   [*CreateResource (D3D11) *](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)
-   [*RotateResourceIdentitiesDXGI*](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)
-   [**D3DDDI \_ ALLOCATIONINFO**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)
-   [**D3D10DDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)
-   [**D3D11DDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)
-   [**DXGI \_ DDI \_ ARG \_ 旋转 \_ 资源 \_ 标识**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_rotate_resource_identities)
-   [**DXGI \_ DDI \_ 显示 \_ 标志**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_present_flags)
-   [**DXGI \_ DDI \_ 主要 \_ DESC**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


鼓励系统构建者使用上述设置测试其立体声驱动程序包，以确保功能正确。

立体声3-d 功能只能在支持 Microsoft DirectX 10 的硬件和更高版本上启用。 但是，因为 Microsoft Direct3D 11 Api 适用于 DirectX 1.x 和2.x 版硬件，所以所有 WDDM 1.2 驱动程序都必须支持 Direct3D 11 并经过全面测试，以确保 Direct3D 11APIs 在所有 Windows 8 硬件上工作。

尽管 stereoscopic 3-d 是可选的 WDDM 1.2 功能，但所有 Windows 8 硬件上都需要 Direct3D 11 API 支持。 因此，WDDM 1.2 驱动程序 (完整图形和渲染设备) 必须通过添加对纹理数组的跨进程共享的支持来支持 Direct3D 11 Api。 此要求用于确保立体声应用在 mono 模式下不会出现故障。

有关硬件设备实现此功能时必须满足的要求的详细信息，请参阅相关 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) ，了解如何 **处理 Stereoscopic 视频内容** 和 **Stereoscopic 3d 模式**。

请参阅 [WDDM 1.2 功能](wddm-v1-2-features.md) ，了解 Windows 8 中添加的功能。

