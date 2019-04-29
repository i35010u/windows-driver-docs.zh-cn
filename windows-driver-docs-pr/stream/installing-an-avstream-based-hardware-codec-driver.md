---
title: 安装基于 AVStream 的硬件编解码器驱动程序
description: 安装基于 AVStream 的硬件编解码器驱动程序
ms.assetid: 7b3bbff7-c8e7-47ea-a455-66f01a552e3b
keywords:
- 硬件编解码器支持 WDK AVStream，安装驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dff4b47ff25c9ac37e7f1c15521ccbbf480d1102
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386499"
---
# <a name="installing-an-avstream-based-hardware-codec-driver"></a>安装基于 AVStream 的硬件编解码器驱动程序


具有硬件支持的编解码器的基于 AVStream 驱动程序应提供类似于其他 AVStream 微型驱动程序的 INF 文件。 但是，有两个硬件供应商可以包括便于特定驱动程序行为的特定条目：

1.  若要指定仅在转码拓扑和播放拓扑中不应使用您的解码器，以下代码添加到驱动程序的 INF 文件中的解码器的 AddReg 部分：

    ```INF
    [shedVideoDecoder.Reader.AddReg]
    HKR,,CLSID,,%Proxy.CLSID%
    HKR,,FriendlyName,,%shedVideoDecoder.Reader.FriendlyName%
    HKR,,MFTMerit,0x00010001,7
    HKR,Capabilities,"{111EA8CD-B62A-4bdb-89F6-67FFCDC2458B}",0x00010001,1
    ```

    前面的代码示例不包括播放拓扑中的解码器。 这可能是必需的硬件供应商已经优化，以便使用其编码器其解码器。

2.  若要启用解码器、 编码器或视频处理器供选择的 Windows Media Player (WMP) 和 Windows 7 转码功能在 shell 中，以下注册表项应设置为 1:

    ```console
    HKLM\Software\Microsoft\WindowsMediaFoundation\HardwareMFT\EnableDecoders
    HKLM\Software\Microsoft\WindowsMediaFoundation\HardwareMFT\EnableEncoders
    HKLM\Software\Microsoft\WindowsMediaFoundation\HardwareMFT\EnableVideoProcessors
    ```
