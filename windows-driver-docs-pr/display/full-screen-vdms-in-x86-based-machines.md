---
title: 基于 x86 的计算机中的全屏 VDM
description: 基于 x86 的计算机中的全屏 VDM
ms.assetid: 5be4919d-d46f-430f-9d4f-670134379268
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，VGA，在基于 x86 的计算机中的全屏幕 Vdm
- VGA WDK 视频微型端口，在基于 x86 的计算机中的全屏幕 Vdm
- 在基于 x86 的计算机 WDK 视频微型端口中的全屏幕 Vdm
- 基于 x86 的计算机兼容的 VGA WDK 的微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dc575de050c7fdf52775ad813a78fdc4885a336
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565791"
---
# <a name="full-screen-vdms-in-x86-based-machines"></a>基于 x86 的计算机中的全屏 VDM


## <span id="ddk_full_screen_vdms_in_x86_based_machines_gg"></span><span id="DDK_FULL_SCREEN_VDMS_IN_X86_BASED_MACHINES_GG"></span>


出于性能原因，当用户在基于 x86 的计算机中，切换到全屏模式的 MS-DOS 应用程序显示驱动程序产生的适配器的控件。 系统的 VGA 或兼容的 VGA 的微型端口驱动程序然后挂钩出 V86 仿真程序中所有 I/O 指令，如应用程序颁发**IN**， **REP INSB/INSW/INSD**， **OUT**，并**REP OUTSB/OUTSW/OUTSD**到视频的 I/O 端口的说明。 这些已挂钩的 I/O 操作转发到兼容的 VGA 的微型端口驱动程序*SvgaHwIoPortXxx*函数。

但是，为了提高性能，微型端口驱动程序可以调用[ **VideoPortSetTrappedEmulatorPorts** ](https://msdn.microsoft.com/library/windows/hardware/ff570366)以允许应用程序直接访问某些 I/O 端口。 微型端口驱动程序将继续挂钩与其他 I/O 端口及其*SvgaHwIoPortXxx*来验证应用程序发出指令流到这些端口。

为了防止提供全屏幕的应用程序发出一系列可能会挂起计算机的说明*SvgaHwIoPortXxx*函数监视应用程序指令流中的驱动程序确定一系列适配器寄存器。 微型端口驱动程序必须启用直接访问仅完全安全的 I/O 端口。 例如，排序器和其他输出寄存器的端口应始终挂接 V86 仿真程序并捕获到的微型端口驱动程序提供*SvgaHwIoPortXxx*函数以进行验证。

直接访问 I/O 端口 （在为 x86 I/O 权限映射） IOPM 的决定应用程序的兼容的 VGA 的微型端口驱动程序通过调用来设置**VideoPortSetTrappedEmulatorPorts**。 请注意微型端口驱动程序可以通过调用此函数可具有访问权限范围，描述 I/O 调整 IOPM 端口、 应用程序发布用于直接访问或到 retrapped *SvgaHwIoPortXxx*函数。 当前 IOPM 确定哪些端口可以由应用程序直接访问，而这仍处于挂接 V86 模拟器并且捕获到*SvgaHwIoPortXxx*函数以进行验证。

默认情况下，设置这样的微型端口驱动程序的仿真程序的访问范围数组中的所有 I/O 端口被截获都放到相应*SvgaHwIoPortXxx*函数。 但是，兼容的 VGA 的微型端口驱动程序通常调用**VideoPortSetTrappedEmulatorPorts** IOCTL 收到\_视频\_启用\_VDM 请求以重置IOPM*VDM*以允许直接访问某些这些 I/O 端口。 通常情况下，此类驱动程序允许直接访问除 VGA sequencer 寄存器和杂项输出寄存器中，所有视频适配器寄存器以及应该始终由验证驱动程序编写器已确定任何 SVGA 特定于适配器的寄存器*SvgaHwIoPortXxx*函数。

 

 





