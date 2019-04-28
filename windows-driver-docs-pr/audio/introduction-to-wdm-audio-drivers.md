---
title: WDM 音频驱动程序简介
description: WDM 音频驱动程序简介
ms.assetid: 376392a8-b3ae-40c3-8bfa-55df6165cefb
keywords:
- 音频筛选器 WDK 的 KS 筛选器的音频，子集
- WDM 音频驱动程序 WDK，有关 WDM 音频驱动程序
- 有关音频驱动程序的音频驱动程序 WDK，
- KS 筛选器 WDK 音频，有关 KS 筛选器
- 筛选器 WDK 音频 KS
- KS pin WDK 音频
- KS pin WDK 音频，有关 KS pin
- pin WDK 音频 KS
- 音频插孔 WDK
- 输出插针 WDK 音频
- 输入插针 WDK 音频
- 筛选器工厂 WDK 音频
- pin 工厂 WDK 音频
- 内核流 WDK 音频
- 筛选器关系图 WDK 音频
- 扬声器 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 072fd3aba8cabda67cc203c4ef198f1680d6d244
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333389"
---
# <a name="introduction-to-wdm-audio-drivers"></a>WDM 音频驱动程序简介


## <span id="introduction_to_wdm_audio_drivers"></span><span id="INTRODUCTION_TO_WDM_AUDIO_DRIVERS"></span>


流式处理 (KS) 内核服务支持内核模式下处理的音频和其他类型的连续媒体中的数据流。 从概念上讲，流进行了处理包含一定数量的处理节点的数据路径，沿流动。 一组相关的节点组合在一起形成*KS 筛选器*，它表示流处理功能的详细信息或无独立块。 可以通过级联到窗体一起多个筛选器的模块化方式构造更复杂的函数*筛选器图形*。

典型的音频适配器卡可能包含用于播放批流通过一系列发言人，来自麦克风的音频信号转换为批流，和合成 MIDI 流中的声音的音频设备。 适配器驱动程序可以包装每个这些音频设备 KS 筛选器，它公开到操作系统中。 操作系统将筛选器连接到其他筛选器处理音频流代表应用程序的窗体筛选器关系图。

KS 筛选器连接在一起，通过其*pin*。 上一个音频筛选器 pin 可以看作的音频插孔。 当客户端需要将数据流路由传入或传出该筛选器时，客户端实例化筛选器上的一个输入或输出插针。 在某些上下文中，术语*pin*并*流*可以互换使用。

上游的筛选器的输出插针连接到下游的筛选器的输入插针。 输出插针从数据流必须输入插针可接受的数据格式。 数据缓冲通常需要消除上一个输出插针所生成的数据和输入插针使用它的费率中的瞬间不匹配。

KS 筛选器作为封装一定数量的相关流处理功能的内核模式驱动程序对象。 在软件或硬件，可以实现的功能。 在此模型中，音频适配器可以视为硬件设备的集合和适配器驱动程序公开的每个作为单个筛选器的音频系统到这些设备。

适配器驱动程序公开一系列*筛选器工厂*到音频系统。 每个筛选器工厂时能够实例化特定类型的筛选器：

-   如果适配器包含类似或相同函数中的一个或多个设备，该驱动程序分组为这些设备的筛选器一起到相同的筛选器工厂。

-   如果适配器包含多种不同类型的设备，这些设备会显示通过多个不同的筛选器工厂。

KS 筛选器公开一系列*固定工厂*到音频系统。 每个 pin 工厂都能够实例化特定类型的 pin。 如果筛选器可以提供相似或相同在函数中，筛选器组的一个或多个 pin 组合在一起这些引脚到相同的 pin 工厂。 例如，可以实例化单个输出插针的一个 pin 工厂和第二个 pin 工厂可以实例化多个输入插针，可能必须执行音频混合的筛选器。

Windows 驱动程序模型为基础构建 KS 服务。 请注意，术语*KS 筛选器*必须是从一词可分辨*筛选器驱动程序*，这是另一个 WDM 概念。 筛选器驱动程序位于 WDM 驱动程序堆栈，并可以截获和修改通过堆栈传播的 I/O 请求数据包 (Irp)。 大写和较低级别筛选器驱动程序分别位于上方和下方函数驱动程序。 在本部分中，术语*筛选器*指 KS 筛选器而不是筛选器驱动程序，除非另有说明。 有关筛选器驱动程序的详细信息，请参阅[WDM 驱动程序类型](https://msdn.microsoft.com/library/windows/hardware/ff564862)。

本部分包含以下主题：

[WDM 音频驱动程序的基本功能](basic-functions-of-a-wdm-audio-driver.md)

[供应商音频驱动程序选项](vendor-audio-driver-options.md)

[WDM 音频术语](wdm-audio-terminology.md)

[示例音频驱动程序](sample-audio-drivers.md)

[KsStudio 实用程序](ksstudio-utility.md)

更新和新功能 WDM 音频体系结构的信息，请参阅[音频技术](https://go.microsoft.com/fwlink/p/?linkid=8751)网站。

 

 




