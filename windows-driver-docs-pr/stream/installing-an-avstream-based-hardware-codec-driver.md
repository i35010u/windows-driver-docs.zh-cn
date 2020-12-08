---
title: 安装基于 AVStream 的硬件编解码器驱动程序
description: 安装基于 AVStream 的硬件编解码器驱动程序
keywords:
- 硬件编解码器支持 WDK AVStream，安装驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40d64e2fdd2e0f2de918ca3a6738cb9e270dabfe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790263"
---
# <a name="installing-an-avstream-based-hardware-codec-driver"></a>安装基于 AVStream 的硬件编解码器驱动程序


具有硬件编解码器支持的基于 AVStream 的驱动程序应提供类似于其他 AVStream 微型驱动程序的 INF 文件。 但是，硬件供应商可以包括两个特定的条目来促进特定驱动程序的行为：

1.  若要指定解码器只应在转码拓扑中使用，而不是在播放拓扑中使用，请将以下内容添加到该驱动程序的 INF 文件中的解码器 AddReg 部分：

    ```INF
    [shedVideoDecoder.Reader.AddReg]
    HKR,,CLSID,,%Proxy.CLSID%
    HKR,,FriendlyName,,%shedVideoDecoder.Reader.FriendlyName%
    HKR,,MFTMerit,0x00010001,7
    HKR,Capabilities,"{111EA8CD-B62A-4bdb-89F6-67FFCDC2458B}",0x00010001,1
    ```

    前面的代码示例在播放拓扑中排除解码器。 这可能是对其解码器进行了优化以使用其编码器的硬件供应商的要求。

2.  若要启用 Windows Media Player (WMP) 和 Windows 7 转码功能在 shell 中选择的解码器、编码器或视频处理器，请将以下注册表项设置为1：

    ```console
    HKLM\Software\Microsoft\WindowsMediaFoundation\HardwareMFT\EnableDecoders
    HKLM\Software\Microsoft\WindowsMediaFoundation\HardwareMFT\EnableEncoders
    HKLM\Software\Microsoft\WindowsMediaFoundation\HardwareMFT\EnableVideoProcessors
    ```
