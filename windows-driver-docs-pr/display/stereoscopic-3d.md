---
title: 立体 3D
description: Windows 8 提供了一致的 API 和设备驱动程序接口 (DDI) 平台立体三维方案，例如游戏和视频播放。
ms.assetid: 2F83E5C6-E333-4BF6-A133-C65A23DAEF62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cc8dde4ab8c427e0701556e6e721ad6ca162f2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545289"
---
# <a name="stereoscopic-3d"></a>立体 3D


Windows 8 提供了一致的 API 和设备驱动程序接口 (DDI) 平台立体三维方案，例如游戏和视频播放。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">Windows 显示器驱动程序模型 (WDDM) 的最低版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最低 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现，完整的图形</td>
<td align="left">可选</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要求和测试</td>
<td align="left"><p><strong>Device.Graphics...ProcessingStereoscopicVideoContent</strong></p>
<p><strong>Device.Display.Monitor.Stereoscopic3DModes</strong></p></td>
</tr>
</tbody>
</table>

 

已有立体的所有组件的系统上仅启用立体三维呈现支持 3 D 的。 这些组件包括支持 3 D 的显示硬件、 图形硬件、 外围设备和软件应用程序。 图形堆栈中的立体声设计是这样的特定可视化效果或使用的显示技术是不可知的操作系统。 显示驱动程序直接与图形显示通信和具有通过标准化的扩展显示标识数据 (EDID) 结构的显示功能有关的知识。 仅当它可以识别此类显示连接到系统时，该驱动程序枚举立体声功能。

若要在显示器微型端口和用户模式驱动程序中实现立体声功能，请参阅新的或更新 DDIs 下面的列表。

立体显示设置属于**屏幕分辨率**控件面板中，如下所示：

![立体显示设置](images/stereo3ddisplaysetting.jpg)

**立体声启用**设置是一个具有以下状态复选框：

-   **不可用**（灰显或不可见）：不支持的呈现音响系统上显示。
-   设置为**已启用**（已选中）：这是能够在立体声显示器上呈现的系统上的默认设置，意味着立体声按需。 默认情况下，桌面窗口管理器 (DWM) 是 mono 的模式。 DWM 会切换到立体声模式仅在时立体声应用将启动由用户 （按需）。 请注意，此复选框被选中时，DWM 可以在 mono 或立体声模式下。
-   设置为**禁用**（未选中）：如果用户具有 DWM 是在 mono 模式下未选中此设置。 在这种情况下，立体声的应用程序提供在 mono 模式下。

## <a name="span-idstereoscopic3-dkernel-modesupportspanspan-idstereoscopic3-dkernel-modesupportspanspan-idstereoscopic3-dkernel-modesupportspanstereoscopic-3-d-kernel-mode-support"></a><span id="Stereoscopic_3-D_kernel-mode_support"></span><span id="stereoscopic_3-d_kernel-mode_support"></span><span id="STEREOSCOPIC_3-D_KERNEL-MODE_SUPPORT"></span>立体三维内核模式下支持


这些 DDIs 会更新 Windows 8 上 VidPN 支持立体三维呈现。

-   [**D3D11DDIARG\_CREATERESOURCE**](https://msdn.microsoft.com/library/windows/hardware/ff542062)
-   [**D3DDDI\_ALLOCATIONINFO**](https://msdn.microsoft.com/library/windows/hardware/ff544364)
-   [**D3DKMDT\_VIDPN\_源\_模式\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff546727)
-   [**D3DKMT\_PRESENTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff548179)
-   [**DXGI\_DDI\_ARG\_旋转\_资源\_标识**](https://msdn.microsoft.com/library/windows/hardware/ff557476)
-   [**DXGK\_PRESENTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff562005)
-   [**DXGK\_SETVIDPNSOURCEADDRESS\_FLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff562052)
-   [**DXGKARG\_OPENALLOCATION**](https://msdn.microsoft.com/library/windows/hardware/ff557609)

## <a name="span-idstereoscopic3-dswapchainddisspanspan-idstereoscopic3-dswapchainddisspanspan-idstereoscopic3-dswapchainddisspanstereoscopic-3-d-swapchain-ddis"></a><span id="Stereoscopic_3-D_swapchain_DDIs"></span><span id="stereoscopic_3-d_swapchain_ddis"></span><span id="STEREOSCOPIC_3-D_SWAPCHAIN_DDIS"></span>立体三维 swapchain DDIs


这些 DDIs 是新的或更新 Windows 8 支持立体三维交换链。

-   [*BltDXGI*](https://msdn.microsoft.com/library/windows/hardware/ff538252)
-   [*Blt1DXGI*](https://msdn.microsoft.com/library/windows/hardware/hh406235)
-   [*CreateResource(D3D10)*](https://msdn.microsoft.com/library/windows/hardware/ff540691)
-   [*CreateResource(D3D11)*](https://msdn.microsoft.com/library/windows/hardware/ff540694)
-   [*RotateResourceIdentitiesDXGI*](https://msdn.microsoft.com/library/windows/hardware/ff569514)
-   [**D3DDDI\_ALLOCATIONINFO**](https://msdn.microsoft.com/library/windows/hardware/ff544364)
-   [**D3D10DDIARG\_CREATERESOURCE**](https://msdn.microsoft.com/library/windows/hardware/ff541697)
-   [**D3D11DDIARG\_CREATERESOURCE**](https://msdn.microsoft.com/library/windows/hardware/ff542062)
-   [**DXGI\_DDI\_ARG\_旋转\_资源\_标识**](https://msdn.microsoft.com/library/windows/hardware/ff557476)
-   [**DXGI\_DDI\_PRESENT\_FLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff557509)
-   [**DXGI\_DDI\_PRIMARY\_DESC**](https://msdn.microsoft.com/library/windows/hardware/ff557511)

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


建议使用上述设置以确保正确功能测试其立体声驱动程序包的系统构建者。

仅在 Microsoft DirectX 10 支持的硬件和更高版本，可以启用立体声的三维功能。 但是，因为 Microsoft Direct3D 11 Api 的 DirectX 9.x 和 10.x 硬件上工作，所有 WDDM 1.2 驱动程序必须支持 Direct3D 11，并全面进行测试以确保 Direct3D 11APIs 所有 Windows 8 硬件上工作。

尽管立体三维是一项可选 WDDM 1.2 功能，但在所有 Windows 8 硬件上需要 Direct3D 11 API 支持。 因此，WDDM 1.2 驱动程序 （所有的图形和渲染设备） 必须通过添加对跨进程共享的纹理数组支持支持 Direct3D 11 Api。 此要求是为了确保立体声应用 mono 模式中不包含故障。

有关实现此功能时，必须满足硬件设备要求的详细信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...处理立体视频内容**并**Device.Display.Monitor.Stereoscopic 3D 模式**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





