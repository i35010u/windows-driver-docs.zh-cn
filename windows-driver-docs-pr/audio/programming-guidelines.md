---
title: HD 音频 DDI 编程指南
description: HD 音频 DDI 编程指南
ms.assetid: 289bdf85-9138-4920-a61f-050c51077d3e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4827dded98bcab494efc207e4174eaef46af9a1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832446"
---
# <a name="hd-audio-ddi-programming-guidelines"></a>HD 音频 DDI 编程指南


本部分介绍使用 HD 音频 DDI 版本（由[**HDAUDIO\_总线\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)、 [**HDAUDIO\_总线\_接口\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)和[**HDAUDIO\_总线定义）的编程准则\_接口\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)结构）控制连接到 HD 音频总线接口控制器的音频和调制解调器编解码器。

HD 音频总线驱动程序将一个或两个版本的 HD 音频 DDI 公开给其子代，它们是音频和调制解调器编解码器的内核模式函数驱动程序。 （其中一个子节点可能是 UAA HD 音频类驱动程序。）这些驱动程序调用 DDIs 中的例程来访问 HD audio 控制器设备的硬件功能。

本部分包括：

[HD audio DDI 版本之间的差异](differences-between-the-hd-audio-ddi-versions.md)

[同步和异步编解码器命令](synchronous-and-asynchronous-codec-commands.md)

[墙壁时钟和链接位置寄存器](wall-clock-and-link-position-registers.md)

[硬件资源管理](hardware-resource-management.md)

[同步两个或多个流](synchronizing-two-or-more-streams.md)

[唤醒启用](wake-enable.md)

[数据复制和缓存策略](data-copying-and-caching-policy.md)

[查询 HD 音频 DDI](querying-for-an-hd-audio-ddi.md)

 

 




