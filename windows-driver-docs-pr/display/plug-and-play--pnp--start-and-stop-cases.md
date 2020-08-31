---
title: WDDM 1.2 和更高版本中的即插即用 (PnP)
description: 所有 Windows 显示驱动程序模型 (WDDM) 1.2 和更高版本的显示微型端口驱动程序必须支持以下行为，以响应启动和停止请求。
ms.assetid: A95DCFEA-BC1B-4A13-9850-13814725D53E
keywords:
- 显示驱动程序中的即插即用 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cef006f8bcfdfa9ce237916ae12f2c8739e0601
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066696"
---
# <a name="plug-and-play-pnp-in-wddm-12-and-later"></a>WDDM 1.2 和更高版本中的即插即用 (PnP)


所有 Windows 显示驱动程序模型 (WDDM) 1.2 和更高版本的显示微型端口驱动程序必须支持以下行为，以响应即插即用 (PnP) 基础结构的启动和停止请求。 行为可能会有所不同，具体取决于驱动程序返回成功还是失败代码，或者系统硬件是否基于基本输入/输出系统 (BIOS) 或统一可扩展固件接口 (UEFI) 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">最小 WDDM 版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现-完整图形和仅显示</td>
<td align="left">必需</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a> 要求和测试</td>
<td align="left"><p><strong>WDDM12. PnpStopStartSupport。</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddisplay_miniport_driver_pnp_ddispanspan-iddisplay_miniport_driver_pnp_ddispanspan-iddisplay_miniport_driver_pnp_ddispandisplay-miniport-driver-pnp-ddi"></a><span id="Display_miniport_driver_PnP_DDI"></span><span id="display_miniport_driver_pnp_ddi"></span><span id="DISPLAY_MINIPORT_DRIVER_PNP_DDI"></span>显示小型端口驱动程序 PnP DDI


从 Windows 8 开始，Microsoft DirectX graphics 内核子系统提供了此函数，当显示设备启动或从休眠中恢复时，驱动程序可以调用此函数：

-   [**DxgkCbAcquirePostDisplayOwnership**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_acquire_post_display_ownership)

这些函数和结构可用于显示微型端口驱动程序以实现 WDDM 1.2 和更高版本的 PnP 要求：

-   [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)
-   [*DxgkDdiSystemDisplayEnable*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_enable)
-   [*DxgkDdiSystemDisplayWrite*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_write)
-   [**DXGK \_ 显示 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_display_information)

## <a name="span-idpnp_start_operationspanspan-idpnp_start_operationspanspan-idpnp_start_operationspanpnp-start-operation"></a><span id="PnP_start_operation"></span><span id="pnp_start_operation"></span><span id="PNP_START_OPERATION"></span>PnP 启动操作


显示设备上的即插即用 (PnP) 启动进程在启动期间或从一个显示驱动程序升级到另一个显示器驱动程序的过程中发生。 在这种情况下，驱动程序必须调用 [*DxgkCbAcquirePostDisplayOwnership*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_acquire_post_display_ownership) 函数以获取有关帧缓冲区的信息并维护显示同步。 帧缓冲区信息是从固件或系统上加载的以前的 WDDM 1.2 和更高版本的驱动程序提供的。

在调用期间，操作系统使[*DxgkDdiSetPowerState*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state)函数返回到 D0 电源状态，在[*DxgkDdiStartDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)函数中，WDDM 1.2 和更高版本的驱动程序必须将源可见性设置为 false ([**DXGKARG \_ SETVIDPNSOURCEVISIBILITY**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourcevisibility)。**Visible**  =  对于所有活动视频呈现网络 (VidPN) 目标，将显示为 "**FALSE**) 。 在这种情况下，显示管道硬件必须与监视器保持同步信号，但不管当前正在扫描的图面中存在哪些像素数据，管道都必须继续将黑色像素数据发送到监视器。这意味着，像素管道保证能用所有黑色像素来遮蔽显示器。 稍后，当第一个帧呈现到帧缓冲区时，操作系统将源可见性设置为 true。

所有这些过程都使监视器保持同步，并确保用户在屏幕上看不到闪烁或闪烁。

这些是驱动程序在 PnP 启动过程之后应返回的返回代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序返回代码</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Success"></span><span id="success"></span><span id="SUCCESS"></span>辉煌</p></td>
<td align="left"><p>行为与 Windows 7 中的行为相同。</p>
<p>对于基于 BIOS 的系统，如果驱动程序已成功启动，则帧缓冲区仍处于活动状态，驱动程序必须准备好将设置为有效模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Failure"></span><span id="failure"></span><span id="FAILURE"></span>否则</p></td>
<td align="left"><p>对于基于 BIOS 的系统，驱动程序必须使系统处于 BIOS 兼容状态。</p>
<p>对于基于 UEFI 的系统，驱动程序必须将显示在 UEFI 图形输出协议设置的同一模式下 (GOP) ，以便基本显示驱动程序可以使用该显示。 驱动程序必须返回有效的错误代码。 如果驱动程序无法使 GOP 处于基本显示驱动程序可以使用的状态，则驱动程序必须从 Ntstatus 返回 <strong>STATUS_GRAPHICS_STALE_MODESET</strong> 错误代码，并且操作系统会导致发生系统检查错误。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idpnp_stop_operationspanspan-idpnp_stop_operationspanspan-idpnp_stop_operationspanpnp-stop-operation"></a><span id="PnP_stop_operation"></span><span id="pnp_stop_operation"></span><span id="PNP_STOP_OPERATION"></span>PnP 停止操作


在将驱动程序升级到新版本时，通常会发生显示设备上的即插即用 (PnP) 停止进程。 在这种情况下，操作系统会调用驱动程序的 [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership) 函数，这需要驱动程序提供准确的帧缓冲区信息。

在[*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)调用中，驱动程序必须确保活动 VidPn 目标的源可见性为 True ([**DXGKARG \_ SETVIDPNSOURCEVISIBILITY**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourcevisibility)。**可见**  =  **TRUE**) 。 此外，从 WDDM 1.2 开始，驱动程序需要确保用黑色像素填充像素管道进行编程以进行扫描的图面。 在将源可见性设置为 true 之前，驱动程序应填写包含黑色像素的图面。

确保还在驱动程序中实现 [*DxgkDdiStopDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device) 。 在某些情况下，操作系统可能会调用 *DxgkDdiStopDevice* 而不是 [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)，或者在对 *DxgkDdiStopDeviceAndReleasePostDisplayOwnership* 的调用失败之后。

这些是驱动程序在 PnP 停止进程之后应返回的返回代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序返回代码</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Success__and_driver_returns_mode_information"></span><span id="success__and_driver_returns_mode_information"></span><span id="SUCCESS__AND_DRIVER_RETURNS_MODE_INFORMATION"></span>成功和驱动程序返回模式信息</p></td>
<td align="left"><p>在停止驱动程序之前，必须使用基本的显示驱动程序使用当前的分辨率来设置帧缓冲区，并且当操作系统调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)"><em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em></a> 函数时，驱动程序必须返回此信息。 保存的模式信息不必与 BIOS 兼容，基本显示器驱动程序在系统重新启动之前不会提供 BIOS 模式。</p>
<p>如果<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)"><em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em></a>返回<strong>STATUS_SUCCESS</strong>，则操作系统保证不会调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device" data-raw-source="[&lt;em&gt;DxgkDdiStopDevice&lt;/em&gt;](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)"><em>DxgkDdiStopDevice</em></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Success__and_driver_sets_the_Width_and_Height_members_of_the_DXGK_DISPLAY_INFORMATION_structure_to_zero"></span><span id="success__and_driver_sets_the_width_and_height_members_of_the_dxgk_display_information_structure_to_zero"></span><span id="SUCCESS__AND_DRIVER_SETS_THE_WIDTH_AND_HEIGHT_MEMBERS_OF_THE_DXGK_DISPLAY_INFORMATION_STRUCTURE_TO_ZERO"></span>成功，驱动程序将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_display_information" data-raw-source="[&lt;strong&gt;DXGK_DISPLAY_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_display_information)"><strong>DXGK_DISPLAY_INFORMATION</strong></a>结构的<strong>宽度</strong>和<strong>高度</strong>成员设置为零</p></td>
<td align="left"><p>仅当系统具有两个图形卡、没有监视器连接到 (当前开机自检) 设备，并且操作系统调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)"><em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em></a> 函数来停止 post 设备时，这种情况才是可能的。</p>
<p>在这种情况下，当前显示器将继续在第二个图形适配器上运行，基本显示驱动程序在支持 POST 设备的适配器上以无外设模式运行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Failure"></span><span id="failure"></span><span id="FAILURE"></span>否则</p></td>
<td align="left"><p>操作系统通过 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device" data-raw-source="[&lt;em&gt;DxgkDdiStopDevice&lt;/em&gt;](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)"><em>DxgkDdiStopDevice</em></a> 函数调用 Windows 7 样式 PnP 停止驱动程序接口。</p>
<p>对于基于 BIOS 的系统，驱动程序必须将显示设置为与 BIOS 兼容的模式。</p>
<p>对于基于 UEFI 的系统，基本显示器驱动程序在图形适配器的无外设模式下运行。</p></td>
</tr>
</tbody>
</table>

 

有关 PnP 和其他状态转换的进一步要求，请参阅 [在 WDDM 1.2 和更高版本中提供无缝状态转换](seamless-state-transitions-in-wddm-1-2-and-later.md)。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅 WHCK 上相关的相关 [文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) 。 **PnpStopStartSupport**。

请参阅 [WDDM 1.2 功能](wddm-v1-2-features.md) ，了解 Windows 8 中添加的功能。

 

