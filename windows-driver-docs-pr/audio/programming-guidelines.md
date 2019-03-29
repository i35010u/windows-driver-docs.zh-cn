---
title: 编程指南
description: 编程指南
ms.assetid: 289bdf85-9138-4920-a61f-050c51077d3e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a3a9803c7f335985abe3baa2929a17d1e9d02a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564658"
---
# <a name="programming-guidelines"></a>编程指南


本部分介绍使用 DDI HD 音频版本的编程指南 (由定义[ **HDAUDIO\_总线\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff536413)， [ **HDAUDIO\_总线\_界面\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)并[ **HDAUDIO\_总线\_接口\_BDL**](https://msdn.microsoft.com/library/windows/hardware/ff536416)结构) 到控制音频和调制解调器的编解码器已连接到 HD Audio 总线界面控制器。

HD Audio 总线驱动程序公开一个或两个版本的 HD 音频 DDI 到其子元素，是用于音频和调制解调器编解码器的内核模式函数驱动程序。 （这些子对象的一个可能是 UAA HD Audio 类驱动程序）。这些驱动程序调用例程在 DDIs 访问 HD Audio 控制器设备的硬件功能。

本部分包括：

[高清晰度音频 DDI 版本之间的差异](differences-between-the-hd-audio-ddi-versions.md)

[同步和异步编解码器命令](synchronous-and-asynchronous-codec-commands.md)

[时钟和链接位置寄存器](wall-clock-and-link-position-registers.md)

[硬件资源管理](hardware-resource-management.md)

[同步两个或多个流](synchronizing-two-or-more-streams.md)

[唤醒启用](wake-enable.md)

[数据复制和缓存策略](data-copying-and-caching-policy.md)

[用于 HD Audio DDI 查询](querying-for-an-hd-audio-ddi.md)

 

 




