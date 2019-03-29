---
title: 验证 SvgaHwIoPortXxx 中的指令
description: 验证 SvgaHwIoPortXxx 中的指令
ms.assetid: 70fe2acb-10ff-4182-96a5-78bff0d8f8a0
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，VGA、 SvgaHwIoPortXxx 函数
- VGA WDK 视频微型端口，SvgaHwIoPortXxx 函数
- SvgaHwIoPortXxx 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f71dff7bcd3a1b74c179e7c6f479525d88d60a32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568362"
---
# <a name="validating-instructions-in-svgahwioportxxx"></a>验证 SvgaHwIoPortXxx 中的指令


## <span id="ddk_validating_instructions_in_svgahwioportxxx_gg"></span><span id="DDK_VALIDATING_INSTRUCTIONS_IN_SVGAHWIOPORTXXX_GG"></span>


如前面所述[兼容的 VGA 的微型端口驱动程序 HwVidFindAdapter](vga-compatible-miniport-driver-s-hwvidfindadapter.md)，IOPM 设置直接访问 I/O 端口通常包括除 sequencer 寄存器和杂项输出注册的所有 SVGA 寄存器其兼容的 VGA 的微型端口驱动程序将继续使用监视其*SvgaHwIoPortXxx*函数。 排序器注册控件内部的芯片计时上兼容的 VGA 视频适配器。 如果全屏幕 MS-DOS 应用程序在同步重置期间涉及其他适配器寄存器，可以挂起计算机。 同样，如果其他输出注册设置为选择不存在的时钟，可以挂起计算机。

兼容的 VGA 的微型端口驱动程序必须确保全屏幕 MS-DOS 应用程序不会发出导致计算机挂起的说明。 每个此类微型端口驱动程序必须提供*SvgaHwIoPortXxx*监视应用程序颁发说明到 I/O 端口的适配器 sequencer 寄存器和杂项函数输出注册。 使用特殊功能的适配器的每个新 VGA 兼容微型端口驱动程序还必须监视并继续验证应用程序可能会将任何可能挂起计算机的指令序列发送到的任何 I/O 端口。

每当应用程序尝试访问 sequencer 时钟寄存器*SvgaHwIoPortXxx*函数必须更改 IOPM 以捕获所有即将在同步重置过程的说明。 只要应用程序发送的指令的影响排序器，或尝试写入其他输出寄存器*SvgaHwIoPortXxx*函数应通过调用调整 IOPM [ **VideoPortSetTrappedEmulatorPorts** ](https://msdn.microsoft.com/library/windows/hardware/ff570366)禁用对所有适配器寄存器的直接访问。

微型端口驱动程序提供*SvgaHwIoPortXxx*函数应缓冲后续**IN** (或**INSB/INSW/INSD**) 和/或**出**（或**OUTSB/OUTSW/OUTSD**) 中的说明**EmulatorAccessEntriesContext**它在视频中设置的区域\_端口\_配置\_信息 （请参阅[兼容的 VGA 的微型端口驱动程序 HwVidFindAdapter](vga-compatible-miniport-driver-s-hwvidfindadapter.md)) 同步重置完成之前，或直到应用程序的其他输出寄存器将还原或重置为"安全"时钟。

然后，微型端口驱动程序负责检查缓冲的说明不能挂起计算机。 如果不是，微型端口驱动程序应处理的缓冲的说明，通常通过调用[ **VideoPortSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff570372)与驱动程序提供[ *HwVidSynchronizeExecutionCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff567369)函数。 否则，微型端口驱动程序应丢弃的缓冲的说明进行操作。

 

 





