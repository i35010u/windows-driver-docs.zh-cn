---
title: WDDM 1.2 和更高版本中的即插即用 (PnP)
description: 若要启动和停止请求的响应中，所有 Windows 显示驱动程序模型 (WDDM) 1.2 和更高版本显示微型端口驱动程序必须都支持以下行为。
ms.assetid: A95DCFEA-BC1B-4A13-9850-13814725D53E
keywords:
- 即插中显示器驱动程序 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f7ea04050b879a58e41dbb6a143e77dbd90756f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366182"
---
# <a name="plug-and-play-pnp-in-wddm-12-and-later"></a>WDDM 1.2 和更高版本中的即插即用 (PnP)


所有 Windows 显示驱动程序模型 (WDDM) 1.2 及更高版本显示微型端口驱动程序必须在启动和停止插即用 (PnP) 基础结构请求的响应中都支持以下行为。 具体取决于是否驱动程序将返回成功或失败的代码，或是否系统硬件基于基本输入/输出系统 (BIOS) 或统一可扩展固件接口 (UEFI)，行为可能不同。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">WDDM 的最低版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现完整的图形和仅显示</td>
<td align="left">强制</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要求和测试</td>
<td align="left"><p><strong>Device.Graphics.WDDM12.Display.PnpStopStartSupport</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddisplayminiportdriverpnpddispanspan-iddisplayminiportdriverpnpddispanspan-iddisplayminiportdriverpnpddispandisplay-miniport-driver-pnp-ddi"></a><span id="Display_miniport_driver_PnP_DDI"></span><span id="display_miniport_driver_pnp_ddi"></span><span id="DISPLAY_MINIPORT_DRIVER_PNP_DDI"></span>显示微型端口驱动程序 PnP DDI


从 Windows 8 开始，Microsoft DirectX 图形内核子系统提供了如果启动或从休眠中恢复的显示设备驱动程序可以调用此函数：

-   [**DxgkCbAcquirePostDisplayOwnership**](https://msdn.microsoft.com/library/windows/hardware/hh451339)

这些函数和结构是可用于显示微型端口驱动程序用于实现 WDDM 1.2 和更高版本的即插即用要求：

-   [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://msdn.microsoft.com/library/windows/hardware/hh451415)
-   [*DxgkDdiSystemDisplayEnable*](https://msdn.microsoft.com/library/windows/hardware/hh451426)
-   [*DxgkDdiSystemDisplayWrite*](https://msdn.microsoft.com/library/windows/hardware/hh451429)
-   [**DXGK\_显示\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh464017)

## <a name="span-idpnpstartoperationspanspan-idpnpstartoperationspanspan-idpnpstartoperationspanpnp-start-operation"></a><span id="PnP_start_operation"></span><span id="pnp_start_operation"></span><span id="PNP_START_OPERATION"></span>PnP 启动操作


显示设备上的插即用 (PnP) 启动进程从一个显示器驱动程序发生启动期间或在升级到另一个。 在这种情况下，驱动程序必须调用[ *DxgkCbAcquirePostDisplayOwnership* ](https://msdn.microsoft.com/library/windows/hardware/hh451339)函数以获取有关帧缓冲区的信息并保持显示同步。 从固件或从上一 WDDM 1.2 和更高版本系统加载的驱动程序提供了帧缓冲区信息。

为此操作系统会在调用期间[ *DxgkDdiSetPowerState* ](https://msdn.microsoft.com/library/windows/hardware/ff560764)函数来返回到 D0 电源状态，并为[ *DxgkDdiStartDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff560775)函数，WDDM 1.2 和更高版本的驱动程序必须设置为 false 的源的可见性 ([**DXGKARG\_SETVIDPNSOURCEVISIBILITY**](https://msdn.microsoft.com/library/windows/hardware/ff559486)。**可见** = **FALSE**) 的所有活动视频存在网络 (VidPN) 目标。 在这种情况下显示管道硬件必须保持同步信号的监视器，但管道必须继续将黑色像素数据发送到哪些像素数据是位于当前正在查看扫描的面无论监视器。这意味着，保证像素管道以将消隐功能使用所有黑色像素的监视器。 更高版本，第一个帧的帧缓冲区呈现时，操作系统将源可见性设置为 true。

这些过程的所有同步的监视器保持和确保用户不会在屏幕上看到闪烁。

这些是驱动程序应返回后即插即用启动过程的返回代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序返回代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Success"></span><span id="success"></span><span id="SUCCESS"></span>成功</p></td>
<td align="left"><p>行为是与 Windows 7 中的相同。</p>
<p>对于基于 BIOS 的系统，如果驱动程序成功启动，帧缓冲区仍处于活动状态，并且驱动程序必须准备好将设置为有效的模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Failure"></span><span id="failure"></span><span id="FAILURE"></span>失败</p></td>
<td align="left"><p>对于基于 BIOS 的系统，该驱动程序必须使系统处于 BIOS 兼容状态。</p>
<p>对于基于 UEFI 的系统，该驱动程序必须将显示保留已设置的 UEFI 图形输出协议 (GOP)，以便基本显示驱动程序可以使用显示在相同模式下。 该驱动程序必须返回有效的错误代码。 如果该驱动程序不能将保留 GOP 基本显示驱动程序可以使用的状态，则驱动程序必须返回<strong>STATUS_GRAPHICS_STALE_MODESET</strong>从 Ntstatus.h 和操作系统错误代码会导致发生系统错误检测.</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idpnpstopoperationspanspan-idpnpstopoperationspanspan-idpnpstopoperationspanpnp-stop-operation"></a><span id="PnP_stop_operation"></span><span id="pnp_stop_operation"></span><span id="PNP_STOP_OPERATION"></span>即插即用的停止操作


显示设备上的插即用 (PnP) 停止进程通常发生在一个驱动程序正在升级到新版本。 在这种情况下操作系统将调用的驱动程序[ *DxgkDdiStopDeviceAndReleasePostDisplayOwnership* ](https://msdn.microsoft.com/library/windows/hardware/hh451415)函数，它需要驱动程序提供准确的帧缓冲区信息。

在中[ *DxgkDdiStopDeviceAndReleasePostDisplayOwnership* ](https://msdn.microsoft.com/library/windows/hardware/hh451415)调用驱动程序必须确保 active VidPn 目标源可见性为 true ([**DXGKARG\_SETVIDPNSOURCEVISIBILITY**](https://msdn.microsoft.com/library/windows/hardware/ff559486)。**可见** = **TRUE**)。 此外，从 WDDM 1.2 驱动程序必须确保像素管道是图面进行编程以扫描出被填充黑色像素。 该驱动程序应完成填充黑色像素在图面之前源可见性设置为 true。

请务必还实现[ *DxgkDdiStopDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff560781)驱动程序中。 操作系统可能会在某些情况下调用*DxgkDdiStopDevice*而不是[ *DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://msdn.microsoft.com/library/windows/hardware/hh451415)，或之后调用*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*失败。

这些是驱动程序应返回后即插即用停止进程的返回代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序返回代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Success__and_driver_returns_mode_information"></span><span id="success__and_driver_returns_mode_information"></span><span id="SUCCESS__AND_DRIVER_RETURNS_MODE_INFORMATION"></span>如果成功和驱动程序返回模式的信息</p></td>
<td align="left"><p>停止该驱动程序之前它必须设置帧缓冲区，使用的当前解析，可以使用基本显示驱动程序，并且该驱动程序必须返回此信息时操作系统将调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh451415" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451415)"> <em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em> </a>函数。 保存的模式信息不一定要与 BIOS，兼容和基本显示驱动程序不会提供 BIOS 模式，直到重新启动系统。</p>
<p>操作系统可保证它不会调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff560781" data-raw-source="[&lt;em&gt;DxgkDdiStopDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560781)"> <em>DxgkDdiStopDevice</em> </a>如果<a href="https://msdn.microsoft.com/library/windows/hardware/hh451415" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451415)"> <em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em> </a>将返回<strong>STATUS_SUCCESS</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Success__and_driver_sets_the_Width_and_Height_members_of_the_DXGK_DISPLAY_INFORMATION_structure_to_zero"></span><span id="success__and_driver_sets_the_width_and_height_members_of_the_dxgk_display_information_structure_to_zero"></span><span id="SUCCESS__AND_DRIVER_SETS_THE_WIDTH_AND_HEIGHT_MEMBERS_OF_THE_DXGK_DISPLAY_INFORMATION_STRUCTURE_TO_ZERO"></span>如果成功和驱动程序集<strong>宽度</strong>并<strong>高度</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh464017" data-raw-source="[&lt;strong&gt;DXGK_DISPLAY_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh464017)"> <strong>DXGK_DISPLAY_INFORMATION</strong> </a>为零的结构</p></td>
<td align="left"><p>仅当系统具有两个图形卡、 没有监视器连接到当前开机自检 (POST) 设备，并且操作系统将调用，这种情况下才可能<a href="https://msdn.microsoft.com/library/windows/hardware/hh451415" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451415)"> <em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em> </a>停止 POST 设备函数。</p>
<p>在当前显示在这种情况下继续运行，在第二个图形适配器上，并支持 POST 设备在适配器上，在无外设模式下运行的基本显示驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Failure"></span><span id="failure"></span><span id="FAILURE"></span>失败</p></td>
<td align="left"><p>操作系统将调用通过 Windows 7 样式即插即用停止驱动程序接口<a href="https://msdn.microsoft.com/library/windows/hardware/ff560781" data-raw-source="[&lt;em&gt;DxgkDdiStopDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560781)"> <em>DxgkDdiStopDevice</em> </a>函数。</p>
<p>对于基于 BIOS 的系统，该驱动程序必须设置为 BIOS 兼容模式显示。</p>
<p>对于基于 UEFI 的系统，基本显示驱动程序运行在图形适配器上的无外设模式下。</p></td>
</tr>
</tbody>
</table>

 

有关进一步上即插即用的要求和其他状态转换，请参阅[提供无缝的状态转换 WDDM 1.2 及更高版本](seamless-state-transitions-in-wddm-1-2-and-later.md)。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics.WDDM12.Display.PnpStopStartSupport**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





