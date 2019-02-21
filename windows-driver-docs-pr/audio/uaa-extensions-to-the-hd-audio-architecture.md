---
title: UAA 扩展到高清晰度音频体系结构
description: UAA 扩展到高清晰度音频体系结构
ms.assetid: 895dc7b6-f484-4be2-8f43-112254d6ef4b
keywords:
- 高清晰度音频，通用音频体系结构
- 高清晰度音频 （HD 音频） 通用音频体系结构
- UAA WDK
- 通用音频体系结构 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1da9370a41fad1c787d476f6a0b96b0fcf52e242
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543318"
---
# <a name="uaa-extensions-to-the-hd-audio-architecture"></a>UAA 扩展到高清晰度音频体系结构


若要符合 UAA，硬件控制器必须实现以下更改*Intel 高定义音频规范*:

-   UAA 设备必须支持 256 条目命令输出环形缓冲区 (CORB) 和响应输入的环形缓冲区 (RIRB)。

此外，Intel HD Audio 体系结构包括多个不需要实现 HD Audio UAA 符合设备的功能。 作为一个选项，硬件供应商可忽略其高清晰度音频设备的下列功能，并保持 UAA 相容状态：

-   DMA 位置较低的基址 (DPLBASE) 和 DMA 位置上部基址 (DPUBASE) 寄存器 （在偏移量 70 h 和 74 h）。

-   即时命令输出，即时响应输入，并立即命令状态注册 （在偏移量 60 h、 64 h 和 68 h）。

-   刷新全局控制寄存器 （在偏移量 08 h) 中的控制位。

总线控制器设计可以省略这些功能，仍可以使用 HD Audio 总线驱动程序完全兼容。 但是，硬件供应商应考虑这些功能是否可能所需的与其他特定于设备的软件的兼容性。 例如，BIOS 例程可以使用即时命令、 响应和状态寄存器。

UAA 版本 1.0，HD Audio 硬件版本必须为 1.0。 （该版本的主版本号和次版本号的 00 h VMAJ 和 VMIN 寄存器即必须指定。）

 

 




