---
title: sAPOs 和 Windows Vista 音频体系结构
description: sAPOs 和 Windows Vista 音频体系结构
ms.assetid: b2effc05-5d5c-4209-b2b3-b91d9f1519e2
keywords:
- LFX WDK
- GFX WDK
- 音频图形 WDK
- 音频引擎 WDK
- 格式协商 WDK 音频
- IsInputFormatSupported WDK
- LockForProcess WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cad644a04ff20596a6bb187c224885379d01ed33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563801"
---
# <a name="sapos-and-the-windows-vista-audio-architecture"></a>sAPOs 和 Windows Vista 音频体系结构


32 位版本的 Windows Server 2003 和 Windows XP 通过使用全局效果筛选器 （GFX 筛选器） 处理数字音频系统效果数据。

操作系统不支持 Windows XP 样式 GFX 筛选器。 相反，Windows Vista 包含默认情况下安装的多个用户模式进程内 COM 对象。 这些对象，称为系统效果音频处理对象 (sAPOs) 提供了 Windows Vista 音频流的数字信号处理。 SAPO 基本上是一个包含一种算法，旨在提供特定的数字信号处理 (DSP) 影响的主机对象。

下图是 Windows Vista 音频体系结构的简化表示形式。 箭头显示流的音频数据的路径。

![说明基本 windows vista 音频体系结构的关系图](images/sysfxapo-ms-components.png)

如图所示，Windows Vista 音频体系结构包括用户模式和内核模式组件。 音频引擎包含流和设备的管道，它从系统提供音频处理对象 (Apo) 和 sAPOs 构建。

内核模式组件具有明确定义每个组件中隔离的功能。

音频的终结点是共同指组件，例如耳机和 loudspeakers。 在关系图中所示，应用程序与通过终结点缓冲区、 流和设备管道和内核模式驱动程序堆栈的音频终结点通信。

中更详细地介绍了概念的管道，不和 sAPOs[探究 Windows Vista 音频引擎](exploring-the-windows-vista-audio-engine.md)主题。 有关系统提供 sAPOs 详细信息，请参阅[Windows 默认不](windows-default-apos.md)主题。

 

 




