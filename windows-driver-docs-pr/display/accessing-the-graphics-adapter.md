---
title: 访问图形适配器
description: 访问图形适配器
keywords:
- 显示驱动程序模型 WDK Windows 2000，图形
- Windows 2000 显示器驱动程序模型 WDK，图形
- 显示驱动程序 WDK Windows 2000，图形
- 图形卡访问 WDK Windows 2000 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5f122262278d601459af71e9d451bc9e5f9ba07
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810557"
---
# <a name="accessing-the-graphics-adapter"></a>访问图形适配器


## <span id="ddk_accessing_the_graphics_adapter_gg"></span><span id="DDK_ACCESSING_THE_GRAPHICS_ADAPTER_GG"></span>


为了确保显示性能，显示器驱动程序可以通过以下方式访问图形卡：

-   间接--通过将 IOCTLs 发送到图形适配器的视频微型端口驱动程序。 请参阅将 [IOCTLs 与视频微型端口驱动程序通信](communicating-ioctls-to-the-video-miniport-driver.md)。

-   直接-通过读取和写入视频内存 (*帧缓冲区*) 或硬件寄存器。 请参阅 [访问帧缓冲区和硬件寄存器](accessing-the-frame-buffer-and-hardware-registers.md)。

 

 





