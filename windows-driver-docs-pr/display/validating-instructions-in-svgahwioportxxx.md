---
title: 验证 SvgaHwIoPortXxx 中的指令
description: 验证 SvgaHwIoPortXxx 中的指令
keywords:
- 视频微型端口驱动程序 WDK Windows 2000、VGA、SvgaHwIoPortXxx 函数
- VGA WDK 视频微型端口，SvgaHwIoPortXxx 函数
- SvgaHwIoPortXxx 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6a7408c3ce9de4d80c9ed96cdbce658e2dbcc70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815413"
---
# <a name="validating-instructions-in-svgahwioportxxx"></a>验证 SvgaHwIoPortXxx 中的指令


## <span id="ddk_validating_instructions_in_svgahwioportxxx_gg"></span><span id="DDK_VALIDATING_INSTRUCTIONS_IN_SVGAHWIOPORTXXX_GG"></span>


正如在与 [Vga 兼容的微型端口驱动程序的 HwVidFindAdapter](vga-compatible-miniport-driver-s-hwvidfindadapter.md)中已提到的那样，IOPM 设置为可直接访问的 i/o 端口通常包含除 sequencer 寄存器和杂项输出寄存器之外的所有 SVGA 注册，VGA 兼容微型端口驱动程序将继续用其 *SvgaHwIoPortXxx* 函数进行监视。 Sequencer 在与 VGA 兼容的视频适配器上注册控制内部芯片计时。 如果全屏 MS-DOS 应用程序在同步重置期间涉及其他适配器注册，计算机可能会挂起。 同样，如果将其他输出寄存器设置为选择不存在的时钟，计算机可能会挂起。

VGA 兼容的微型端口驱动程序必须确保全屏 MS-DOS 应用程序不会发出导致计算机挂起的指令。 每个这样的微型端口驱动程序都必须提供 *SvgaHwIoPortXxx* 函数，这些函数可监视应用程序发出的有关适配器 sequencer 寄存器和杂项输出寄存器的 i/o 端口的指令。 具有特殊功能的适配器的每个新的 VGA 兼容微型端口驱动程序也必须监视并继续验证任何 i/o 端口，应用程序可能会将任何可能会挂起计算机的指令序列发送到该端口。

当应用程序尝试访问 sequencer 时钟寄存器时， *SvgaHwIoPortXxx* 函数必须更改 IOPM，以捕获同步重置过程中传入的所有指令。 一旦应用程序发送了影响 sequencer 或尝试写入杂项输出寄存器的指令， *SvgaHwIoPortXxx* 函数应通过调用 [**VideoPortSetTrappedEmulatorPorts**](/windows-hardware/drivers/ddi/video/nf-video-videoportsettrappedemulatorports) 来禁用对所有适配器寄存器的直接访问，从而调整 IOPM。

微型端口驱动程序提供 *的 SvgaHwIoPortXxx* 函数应在 (或 **INSB/INSW/INSD**) 和/或 **OUT** (或 **OUTSB** /OUTSW **中的后续部分****中** 进行缓冲) 说明在视频 \_ 端口配置信息中设置 \_ \_ (参阅 [VGA 兼容的微型端口驱动程序的 outsb](vga-compatible-miniport-driver-s-hwvidfindadapter.md)) 直到同步重置完成为止。或者，直到应用程序还原杂项输出寄存器或将其重置为 "safe" 时钟。

然后，微型端口驱动程序负责检查缓冲的指令是否无法挂起计算机。 如果不是这样，微型端口驱动程序应处理缓冲的指令，通常通过使用驱动程序提供的 [*HwVidSynchronizeExecutionCallback*](/windows-hardware/drivers/ddi/video/nc-video-pminiport_synchronize_routine)函数调用 [**VideoPortSynchronizeExecution**](/windows-hardware/drivers/ddi/video/nf-video-videoportsynchronizeexecution) 。 否则，微型端口驱动程序应丢弃缓冲的指令。

 

