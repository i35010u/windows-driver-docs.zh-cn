---
title: 针对 HD 音频体系结构的 UAA 扩展
description: 针对 HD 音频体系结构的 UAA 扩展
keywords:
- HD 音频，通用音频体系结构
- 高清晰音频 (HD 音频) ，通用音频体系结构
- UAA WDK
- 通用音频体系结构 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63f01c0d5b6d830423fc8621ae3773ce1e14bb96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800485"
---
# <a name="uaa-extensions-to-the-hd-audio-architecture"></a>针对 HD 音频体系结构的 UAA 扩展


若要符合 UAA，硬件控制器必须实现对 *Intel 高质音频规范* 的以下更改：

-   UAA 设备必须支持256项，每个 (CORB) 和响应输入环形缓冲区 (RIRB) 。

此外，Intel HD 音频体系结构还包括实现 UAA 兼容的 HD 音频设备不需要的多个功能。 作为一个选项，硬件供应商可以从其 HD 音频设备中省略以下功能，并保持与 UAA 兼容：

-   DMA 位置下限基址 (DPLBASE) 和 DMA 位置上基址 (DPUBASE) 在偏移量70h 和 74h (注册) 。

-   即时命令输出、立即响应输入和即时命令状态在偏移60h、64h 和 68h) 上注册 (。

-   全局控件寄存器中的 "刷新" 控制位 () 偏移量08h。

总线控制器设计可以省略这些功能，并且仍与 HD 音频总线驱动程序完全兼容。 但是，硬件供应商应该考虑是否需要这些功能才能与其他特定于设备的软件兼容。 例如，BIOS 例程可能使用即时命令、响应和状态寄存器。

对于 UAA 版本1.0，HD 音频硬件版本必须为1.0。  (VMAJ 和 VMIN 寄存器必须指定第01h 版本号和次版本号为00h。 ) 

 

 




