---
title: 在 WDDM 1.2 和更高版本中提供无缝状态转换
description: 有多种功能有助于最大程度地减少启动过程中的屏幕闪烁、从较低的电源状态转换和转换回操作系统控制。
keywords:
- 状态转换 WDK 显示
- 从休眠 WDK 显示恢复
- 显示驱动程序中的固件模式 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c31c6df2ec1fa293843c085fdda389923c36374
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816827"
---
# <a name="providing-seamless-state-transitions-in-wddm-12-and-later"></a>在 WDDM 1.2 和更高版本中提供无缝状态转换


从 Windows 8 开始，多项功能有助于最大程度地减少或消除启动过程中的屏幕闪烁和闪烁、在从较低的电源状态转换到期间，以及转换回驱动程序升级或系统 bug 检查中的操作系统控制期间。 此外，Windows 8 及更高版本的计算机上的系统固件必须在开机时检测集成显示面板的本机分辨率和时间，并将此信息移交给操作系统。 Windows 显示驱动程序模型 (WDDM) 1.2 和更高版本的显示微型端口驱动程序必须支持此行为。

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
<td align="left"><a href="/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a> 要求和测试</td>
<td align="left"><p><strong>System.web...。</strong></p>
<p><strong>设备 .。。PnpStopStartSupport</strong></p>
<p><strong>设备 .。。DisplayOutputControl</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtransition_from_firmware_to_operating_systemspanspan-idtransition_from_firmware_to_operating_systemspanspan-idtransition_from_firmware_to_operating_systemspantransition-from-firmware-to-operating-system"></a><span id="Transition_from_firmware_to_operating_system"></span><span id="transition_from_firmware_to_operating_system"></span><span id="TRANSITION_FROM_FIRMWARE_TO_OPERATING_SYSTEM"></span>从固件过渡到操作系统


所有面向客户端 Sku 的 Windows 8 系统都必须支持 (UEFI) 图形输出协议 (GOP) 的统一可扩展固件接口。 在启动阶段，GOP 在系统的集成显示面板上设置本机计时和本机分辨率。 当操作系统准备接管显示的所有权时，GOP 会直接退出帧缓冲区，该缓冲区可用于向外浏览。 此时，操作系统不会尝试重置显示时间或解决方法，而只是使用提供的帧缓冲区，从而消除了一个屏幕闪烁。

**硬件认证要求**

有关硬件设备实现此功能时必须满足的要求的信息，请参阅 WHCK **上的** 相关 [文档](/windows-hardware/test/hlk/windows-hardware-lab-kit)。

## <a name="span-idtransition_from_operating_system_to_driverspanspan-idtransition_from_operating_system_to_driverspanspan-idtransition_from_operating_system_to_driverspantransition-from-operating-system-to-driver"></a><span id="Transition_from_operating_system_to_driver"></span><span id="transition_from_operating_system_to_driver"></span><span id="TRANSITION_FROM_OPERATING_SYSTEM_TO_DRIVER"></span>从操作系统转换为驱动程序


在启动后，当操作系统将显示的所有权移交给 WDDM 驱动程序时，它会通过调用 [*DxgkDdiStartDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device) 函数启动即插即用 (PnP) 设备的启动。 或者，在从休眠状态恢复后，操作系统将调用 [*DxgkDdiSetPowerState*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state) 函数来启动设备，并将 *DeviceUid* 参数设置为显示 (在) 中定义的 **\_ 适配器 \_ HW \_ ID** 。 此时，在 WDDM 图形驱动程序控制的同时， (呈现为黑色) ，这通常会遮蔽屏幕。

驱动程序可以从 Windows 8) 中启动 (调用 [**DxgkCbAcquirePostDisplayOwnership**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_acquire_post_display_ownership) 函数，以便在操作系统中查询当前帧缓冲区的确切状态以及固件和启动加载程序设置的显示模式。 通过此函数检索到的 [**DXGK \_ 显示 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_display_information) 结构中的信息，驱动程序可以使显示控制器保持活动状态，而不会导致监视器重新同步。 由于驱动程序还包含有关帧缓冲区的详细信息，因此可以执行更平稳的转换。

在 [WDDM 1.2 和更高版本中，即插即用 (pnp) ](plug-and-play--pnp--start-and-stop-cases.md)提供了有关 pnp 启动的更多详细信息。

## <a name="span-idtransition_from_driver_to_operating_systemspanspan-idtransition_from_driver_to_operating_systemspanspan-idtransition_from_driver_to_operating_systemspantransition-from-driver-to-operating-system"></a><span id="Transition_from_driver_to_operating_system"></span><span id="transition_from_driver_to_operating_system"></span><span id="TRANSITION_FROM_DRIVER_TO_OPERATING_SYSTEM"></span>从驱动程序转换为操作系统


操作系统可以通过调用 [*DxgkDdiStopDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device) 函数请求显示设备的 PnP 停止。 此时，在操作系统接管显示控制时， (呈现为黑色) ，这通常会遮蔽屏幕。 操作系统可以从 Windows 8) 中启动 (调用 [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership) 函数，该函数要求 WDDM 驱动程序设置配置用于扫描的帧缓冲区。操作系统可以在此帧缓冲区内呈现，同时控制其显示，使其可以执行平滑转换。

在 [WDDM 1.2 和更高版本中，即插即用 (pnp) ](plug-and-play--pnp--start-and-stop-cases.md)提供了有关 PnP 停止的更多详细信息，包括其他方案。

**硬件认证要求**

有关此移交的详细信息，请参阅相关 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) **PnpStopStartSupport**。

## <a name="span-idtransition_to_operating_system_without_disabling_driverspanspan-idtransition_to_operating_system_without_disabling_driverspanspan-idtransition_to_operating_system_without_disabling_driverspantransition-to-operating-system-without-disabling-driver"></a><span id="Transition_to_operating_system_without_disabling_driver"></span><span id="transition_to_operating_system_without_disabling_driver"></span><span id="TRANSITION_TO_OPERATING_SYSTEM_WITHOUT_DISABLING_DRIVER"></span>在不禁用驱动程序的情况下过渡到操作系统


有时，操作系统会遇到不可恢复的错误，并且必须发出系统 bug 检查。 发生这种情况时，某些情况下操作系统必须控制显示，但不能停止 WDDM 驱动程序。 需要使用 WDDM 1.2 和更高版本的驱动程序来实现 [*DxgkDdiSystemDisplayEnable*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_enable) 和 [*DxgkDdiSystemDisplayWrite*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_write) 函数，使操作系统可以无缝地将其转换为可在其中显示错误屏幕的状态，同时保持图形界面高分辨率和颜色深度。 此过渡消除了 jarring 的用户体验。

**硬件认证要求**

有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) **DisplayOutputControl**。

## <a name="span-idwindows_8_firmware_mode_changesspanspan-idwindows_8_firmware_mode_changesspanspan-idwindows_8_firmware_mode_changesspanwindows-8-firmware-mode-changes"></a><span id="Windows_8_firmware_mode_changes"></span><span id="windows_8_firmware_mode_changes"></span><span id="WINDOWS_8_FIRMWARE_MODE_CHANGES"></span>Windows 8 固件模式更改


在固件向操作系统移交控制权之前，会更改固件的显示模式：

<span id="_1.2_and_later_drivers__dxgkddi_interface_version____dxgkddi_interface_version_win8_"></span><span id="_1.2_AND_LATER_DRIVERS__DXGKDDI_INTERFACE_VERSION____DXGKDDI_INTERFACE_VERSION_WIN8_"></span>WDDM 1.2 和更高版本的驱动程序 (**DXGKDDI \_ 接口 \_ 版本** &gt; =  **DXGKDDI \_ 接口 \_ 版本 \_ WIN8**)   
为了进一步消除显示闪烁，从 Windows 8 开始，不会在 WDDM 1.2 和更高版本驱动程序的固件上调用 Int10 模式更改请求。

此外，如果在关闭监视器后发生模式更改，操作系统只调用 [*DxgkDdiCommitVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)函数一次，并将 *pCommitVidPnArg* 参数设置为它在监视器已打开时的值，并将 *pCommitVidPnArg* 标志的 **PathPoweredOff** 成员 - &gt; **Flags** 设置为 **TRUE**。

<span id="_1.0_and_1.1_drivers__DXGKDDI_INTERFACE_VERSION___DXGKDDI_INTERFACE_VERSION_WIN8_"></span><span id="_1.0_and_1.1_drivers__dxgkddi_interface_version___dxgkddi_interface_version_win8_"></span><span id="_1.0_AND_1.1_DRIVERS__DXGKDDI_INTERFACE_VERSION___DXGKDDI_INTERFACE_VERSION_WIN8_"></span>WDDM 1.0 和1.1 驱动程序 (**DXGKDDI \_ 接口 \_ 版本** &lt; **DXGKDDI \_ 接口 \_ 版本 \_ WIN8**)   
对于在 Windows 8 上运行的 WDDM 版本1.0 和1.1 驱动程序，在启动过程中或从休眠中恢复时，会将调入 Int10 VGA 模式，使其将显示分辨率设置为监视器的本机高分辨率。 在 Windows 8 之前，Int10 VGA mode 0x12 调用将显示分辨率设置为 640 x 480 像素，每像素16位，无闪烁光标，以显示操作系统初始屏幕图像。

但是，对于指示它们不支持高分辨率模式的 WDDM 版本1.0 和1.1 驱动程序，从 Windows 8 启动到 VGA 模式0x12 将显示分辨率设置为 640 x 480 像素，每像素16位，无闪烁的光标。 当系统从休眠恢复时，显示分辨率仍将设置为监视器的本机高分辨率。

此外，如果在关闭监视器后发生模式更改，则操作系统会按上述针对 WDDM 1.2 驱动程序的 [*DxgkDdiCommitVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)函数进行调用，另外，它会 *再次* 调用 *DxgkDdiCommitVidPn* *pCommitVidPnArg* hFunctionalVidPn 中的空视频 (VidPN) - &gt; **hFunctionalVidPn** ，而不是 *pCommitVidPnArg* 标志中设置的任何标志值 - &gt; **Flags**。

如果在休眠后恢复系统，并且监视同步生成仍处于启用状态，则也会发生这两个部分的调用序列。 在这种情况下，当驱动程序收到第二次调用 [*DxgkDdiCommitVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)时，该驱动程序应不执行任何操作。

