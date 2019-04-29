---
title: 访问图形适配器
description: 访问图形适配器
ms.assetid: 85c99b4b-690c-49f1-b6ed-4b72b6049026
keywords:
- 显示器驱动程序模型 WDK Windows 2000 中，图形
- Windows 2000 显示器驱动程序模型 WDK，图形
- 显示驱动程序 WDK Windows 2000 中，图形
- 图形卡访问 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bfde5bd300e5e96b476078a714cef00629f93a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387901"
---
# <a name="accessing-the-graphics-adapter"></a>访问图形适配器


## <span id="ddk_accessing_the_graphics_adapter_gg"></span><span id="DDK_ACCESSING_THE_GRAPHICS_ADAPTER_GG"></span>


若要确保显示的性能，显示器驱动程序可以按以下方式访问图形卡：

-   间接-通过将 Ioctl 发送到图形适配器的微型端口驱动程序。 请参阅[通信到视频微型端口驱动程序 Ioctl](communicating-ioctls-to-the-video-miniport-driver.md)。

-   直接-由对视频内存读取和写入 (*帧缓冲区*) 或硬件寄存器。 请参阅[访问的帧缓冲区和硬件注册](accessing-the-frame-buffer-and-hardware-registers.md)。

 

 





