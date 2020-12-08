---
title: HD 音频 DDI 编程指南
description: HD 音频 DDI 编程指南
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cb710e2be9bf46bd44be803781223004054672a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800787"
---
# <a name="hd-audio-ddi-programming-guidelines"></a>HD 音频 DDI 编程指南


本部分提供了使用 [**HDAUDIO \_ 总线 \_ 接口**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)（ [**HDAUDIO \_ 总线 \_ 接口 \_ V2**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2) 和 [**HDAUDIO \_ 总线 \_ 接口 \_ BDL**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl) 结构）定义的 HD 音频 DDI (版本的编程准则，) 控制连接到 HD 音频总线接口控制器的音频和调制解调器编解码器。

HD 音频总线驱动程序将一个或两个版本的 HD 音频 DDI 公开给其子代，它们是音频和调制解调器编解码器的内核模式函数驱动程序。  (其中一个子节点可能是 UAA HD 音频类驱动程序。 ) 这些驱动程序调用 DDIs 中的例程来访问 HD audio 控制器设备的硬件功能。

本节包括：

[HD 音频 DDI 版本之间的差异](differences-between-the-hd-audio-ddi-versions.md)

[同步和异步编解码器命令](synchronous-and-asynchronous-codec-commands.md)

[时钟和链接位置寄存器](wall-clock-and-link-position-registers.md)

[硬件资源管理](hardware-resource-management.md)

[同步两个或多个流](synchronizing-two-or-more-streams.md)

[启用唤醒](wake-enable.md)

[数据复制和缓存策略](data-copying-and-caching-policy.md)

[查询 HD 音频 DDI](querying-for-an-hd-audio-ddi.md)

 

