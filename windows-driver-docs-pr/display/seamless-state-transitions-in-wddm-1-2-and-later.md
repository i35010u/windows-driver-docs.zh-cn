---
title: 提供无缝的状态转换 WDDM 1.2 及更高版本
description: 多项功能有助于最大程度减少屏幕闪烁，在引导过程、 从较低的电源状态转换以及转换返回到操作系统控制。
ms.assetid: CD2208AA-62B6-4BAD-BE7C-0791B13D1E96
keywords:
- 状态转换 WDK 显示
- 从休眠状态 WDK 显示恢复
- 中的固件模式显示驱动程序 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 110fad8e532db83f0010651275cc867add39de5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547734"
---
# <a name="providing-seamless-state-transitions-in-wddm-12-and-later"></a>提供无缝的状态转换 WDDM 1.2 及更高版本


从开始 Windows 8 中，多个功能帮助以最大程度减少或消除屏幕闪烁和闪烁在启动过程中，从较低的电源状态，进行转换时和进行转换时返回到操作系统中的控件驱动程序升级或系统错误检查。 此外，Windows 8 和更高版本的计算机上的系统固件必须检测到自身分辨率和计时的集成了电源时显示面板并将提交给系统的此信息。 Windows 显示驱动程序模型 (WDDM) 1.2 和更高版本显示微型端口驱动程序必须支持此行为。

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
<td align="left">最低 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现 — 仅完全图形和显示</td>
<td align="left">强制</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要求和测试</td>
<td align="left"><p><strong>System.Client.Firmware.UEFI.GOP.Display</strong></p>
<p><strong>Device.Graphics…PnpStopStartSupport</strong></p>
<p><strong>Device.Graphics...DisplayOutputControl</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtransitionfromfirmwaretooperatingsystemspanspan-idtransitionfromfirmwaretooperatingsystemspanspan-idtransitionfromfirmwaretooperatingsystemspantransition-from-firmware-to-operating-system"></a><span id="Transition_from_firmware_to_operating_system"></span><span id="transition_from_firmware_to_operating_system"></span><span id="TRANSITION_FROM_FIRMWARE_TO_OPERATING_SYSTEM"></span>固件从过渡到操作系统


针对客户端 Sku 的所有 Windows 8 系统必须都支持统一可扩展固件接口 (UEFI) 的图形输出协议 (GOP)。 在启动阶段，GOP 本机计时和自身分辨率上设置的系统集成的显示面板。 准备好接管其所有权的显示操作系统时，关闭 GOP 可用于扫描出到显示的帧缓冲区。 在这一次操作系统不会尝试重置显示计时或分辨率，但只需使用提供的帧缓冲区，从而消除一个屏幕闪烁。

**硬件认证要求**

有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**System.Client.Firmware.UEFI.GOP.Display**。

## <a name="span-idtransitionfromoperatingsystemtodriverspanspan-idtransitionfromoperatingsystemtodriverspanspan-idtransitionfromoperatingsystemtodriverspantransition-from-operating-system-to-driver"></a><span id="Transition_from_operating_system_to_driver"></span><span id="transition_from_operating_system_to_driver"></span><span id="TRANSITION_FROM_OPERATING_SYSTEM_TO_DRIVER"></span>从操作系统过渡到驱动程序


当操作系统启动后将显示的所有权传递给 WDDM 驱动程序时，它启动设备插即用 (PnP) 开始通过调用[ *DxgkDdiStartDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff560775)函数。 或者，从休眠状态恢复后在操作系统启动设备通过调用[ *DxgkDdiSetPowerState* ](https://msdn.microsoft.com/library/windows/hardware/ff560764)函数与*DeviceUid*参数设置为**DISPLAY\_适配器\_HW\_ID** （Video.h 中定义）。 在此时间通常屏幕是留空 （将呈现为黑色） 同时 WDDM 图形驱动程序控制。

该驱动程序可以调用[ **DxgkCbAcquirePostDisplayOwnership** ](https://msdn.microsoft.com/library/windows/hardware/hh451339)查询适用于当前的帧缓冲区和显示的准确状态函数 （可从 Windows 8）固件和启动加载器已设置的模式。 使用中的信息[ **DXGK\_显示\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh464017)结构检索此函数，就可以保持显示控制器处于活动状态的驱动程序和不会导致监视器的重新同步。 因为该驱动程序还详细介绍了帧缓冲区，则可以执行更流畅的转换。

即插即用开始上的更多详细信息中提供了[插 (PnP) WDDM 1.2 及更高版本](plug-and-play--pnp--start-and-stop-cases.md)。

## <a name="span-idtransitionfromdrivertooperatingsystemspanspan-idtransitionfromdrivertooperatingsystemspanspan-idtransitionfromdrivertooperatingsystemspantransition-from-driver-to-operating-system"></a><span id="Transition_from_driver_to_operating_system"></span><span id="transition_from_driver_to_operating_system"></span><span id="TRANSITION_FROM_DRIVER_TO_OPERATING_SYSTEM"></span>从驱动程序转换到操作系统


操作系统可以通过调用请求显示设备的即插即用停止[ *DxgkDdiStopDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff560781)函数。 在此时间通常屏幕是留空 （将呈现为黑色） 时，操作系统会显示控件上。 操作系统可以调用[ *DxgkDdiStopDeviceAndReleasePostDisplayOwnership* ](https://msdn.microsoft.com/library/windows/hardware/hh451415)需要 WDDM 驱动程序设置为配置的帧缓冲区的函数 （可从 Windows 8）扫描出。在控件的显示，从而可以执行的平稳转换时，操作系统可以呈现到此帧缓冲区。

即插即用停止，包括其他方案的更多详细信息中提供了[插 (PnP) WDDM 1.2 及更高版本](plug-and-play--pnp--start-and-stop-cases.md)。

**硬件认证要求**

有关此切换的详细信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...PnpStopStartSupport**。

## <a name="span-idtransitiontooperatingsystemwithoutdisablingdriverspanspan-idtransitiontooperatingsystemwithoutdisablingdriverspanspan-idtransitiontooperatingsystemwithoutdisablingdriverspantransition-to-operating-system-without-disabling-driver"></a><span id="Transition_to_operating_system_without_disabling_driver"></span><span id="transition_to_operating_system_without_disabling_driver"></span><span id="TRANSITION_TO_OPERATING_SYSTEM_WITHOUT_DISABLING_DRIVER"></span>转换到操作系统，但不能禁用驱动程序


有时操作系统遇到不可恢复的错误，且需要发出检查系统错误。 在此情况下，有某些情况下，操作系统必须显示的控制，但没有停止 WDDM 驱动程序的功能。 WDDM 1.2 和更高版本的驱动程序所需实现[ *DxgkDdiSystemDisplayEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh451426)并[ *DxgkDdiSystemDisplayWrite* ](https://msdn.microsoft.com/library/windows/hardware/hh451429)函数，它允许操作系统无缝过渡到它可以保持在高分辨率和颜色深度的图形界面的同时显示错误屏幕的状态。 此转换可消除不和谐的用户体验。

**硬件认证要求**

有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...DisplayOutputControl**。

## <a name="span-idwindows8firmwaremodechangesspanspan-idwindows8firmwaremodechangesspanspan-idwindows8firmwaremodechangesspanwindows8-firmware-mode-changes"></a><span id="Windows_8_firmware_mode_changes"></span><span id="windows_8_firmware_mode_changes"></span><span id="WINDOWS_8_FIRMWARE_MODE_CHANGES"></span>Windows 8 固件模式更改


以下是对固件移交给系统的控件之前的固件的显示模式的更改：

<span id="_1.2_and_later_drivers__dxgkddi_interface_version____dxgkddi_interface_version_win8_"></span><span id="_1.2_AND_LATER_DRIVERS__DXGKDDI_INTERFACE_VERSION____DXGKDDI_INTERFACE_VERSION_WIN8_"></span>WDDM 1.2 和更高版本的驱动程序 (**DXGKDDI\_界面\_版本** &gt; =  **DXGKDDI\_接口\_版本\_WIN8**)  
若要进一步消除显示闪烁，从 Windows 8 开始 Int10 模式更改请求在时不调用固件 WDDM 1.2 和更高版本的驱动程序。

此外，如果模式更改时，监视器处于关闭状态，操作系统将调用[ *DxgkDdiCommitVidPn* ](https://msdn.microsoft.com/library/windows/hardware/ff559597)函数一次，与*pCommitVidPnArg*参数设置为值时，监视器已开启，并**PathPoweredOff**的成员*pCommitVidPnArg* - &gt; **标志**设置为 **，则返回 TRUE**。

<span id="_1.0_and_1.1_drivers__DXGKDDI_INTERFACE_VERSION___DXGKDDI_INTERFACE_VERSION_WIN8_"></span><span id="_1.0_and_1.1_drivers__dxgkddi_interface_version___dxgkddi_interface_version_win8_"></span><span id="_1.0_AND_1.1_DRIVERS__DXGKDDI_INTERFACE_VERSION___DXGKDDI_INTERFACE_VERSION_WIN8_"></span>WDDM 1.0 和 1.1 驱动程序 (**DXGKDDI\_界面\_版本** &lt; **DXGKDDI\_接口\_版本\_WIN8**)  
对于 WDDM 版本 1.0 和 1.1 驱动程序在 Windows 8 上运行，在启动过程中或从休眠恢复时进入 Int10 VGA 模式 0x12 的调用，到监视器的高分辨率设置显示分辨率。 在 Windows 8 之前 Int10 VGA 模式 0x12 调用设置为 640 x 480 像素，在 16 位 / 像素，以显示操作系统初始屏幕图像无闪烁光标的显示分辨率。

但是，WDDM 版本 1.0 和 1.1 指示它们不支持高分辨率模式下，从启动到 VGA 模式 0x12 开始 Windows 8 中的驱动程序将显示分辨率设为 640 x 480 像素，在 16 位 / 像素，与任何闪烁的光标。 当从休眠中恢复系统时，显示分辨率将仍设置为监视器的高分辨率。

此外，如果模式更改时，监视器处于关闭状态，操作系统将调用[ *DxgkDdiCommitVidPn* ](https://msdn.microsoft.com/library/windows/hardware/ff559597)函数上文所述的 WDDM 1.2 驱动程序，以及它将调用*DxgkDdiCommitVidPn* *第二个*中的时间与空视频存在网络 (VidPN) *pCommitVidPnArg* - &gt; **hFunctionalVidPn** ，且未设置的值的标志*pCommitVidPnArg*-&gt;**标志**。

系统恢复后休眠和监视器同步生成，要保持启用状态时，也会发生此调用两部分组成的序列。 在这种情况下，驱动程序应执行任何操作，在接收到第二次调用时[ *DxgkDdiCommitVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559597)。

 

 





