---
title: SysTray 和 SndVol32
description: SysTray 和 SndVol32
keywords:
- 托盘乐曲音频
- SndVol32 WDK 音频
- 主音量设置 WDK 音频
- 扬声器 WDK 音频，图标显示
- 卷设置 WDK 音频
- 图标 WDK 音频
- 显示扬声器图标
- 音量滑块 WDK 音频
- 隐藏的扬声器图标 WDK 音频
- 静音控制 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35ddc6c9fa79a5091aaef983c749ed7d71891b20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800529"
---
# <a name="systray-and-sndvol32"></a>SysTray 和 SndVol32


## <span id="systray_and_sndvol32"></span><span id="SYSTRAY_AND_SNDVOL32"></span>


SndVol32 程序 ( # A0) 控制各种声音 (源的卷设置，如波形、CD 和合成器) 和主音量设置。 SndVol32 程序表示为显示在任务栏通知区域中的扬声器图标，任务栏在默认情况下显示在 Windows 屏幕的右下角。

 ( # A0) 的系统托盘程序负责显示扬声器图标（当它处于打开状态时），并在关闭扬声器图标时将其隐藏。 在 Windows XP 中，默认情况下，扬声器图标处于隐藏状态。 在所有其他 Windows 版本（包括 Windows XP SP1）中，默认情况下，扬声器图标可见。

在 Windows XP 中，按照以下步骤在任务栏上显示扬声器图标：

1.  在 "控制面板" 中，单击 " **声音和音频设备** " 图标 (或只需 mmsys.cpl) 运行。

2.  在 " **卷** " 选项卡上，选中 " **任务栏中的图标** " 复选框。

如果声卡的音量级别可以在 "软件控制" 下更改，则任务栏上会显示一个扬声器图标。 您可以通过单击该图标并调整音量滑块来更改 "主要容量" 设置。

在登录时，使用 MIXERLINE \_ COMPONENTTYPE \_ dst \_ 扬声器 (扬声器目标) 或 MIXERLINE \_ COMPONENTTYPE \_ dst \_ 耳机 (耳机目标) 组件类型来确定是否应显示扬声器图标，在登录时，托盘将查询音频驱动程序。 如果这两个组件类型均未找到，则托盘不会显示扬声器图标。 如果找到该行，它会查询该行以确定它是否包含静音控件。 通过在内部存储 " **行 ID** " 和 " **静音" 控件 ID** 以供将来参考，托盘完成其登录时混音器。

SndVol32 程序还提供了用于控制系统中所有卷控件的用户界面。 如果用户双击系统任务栏中的扬声器图标 (或只是 Sndvol32.exe) 运行，则 SndVol32 将显示 "主音量" 窗口，其中包含用于控制各种声音源上的主音量级别和音量级别的滑块。 在这种情况下，SndVol32 使用不同的算法来确定所显示的内容。 对于 " **主音量" 滑块**，它会在 "主" 目标上查找第一个音量控件 (例如，编号为零的目标) 。 这通常是发言人目标。

当 SndVol32 运行时，它会查询混音器驱动程序，寻找一组它知道的一组控件。 若要显示滑块面板，源行应至少具有以下控件之一：

-   音量控制

-   静音控件

-   高级控制 (AGC、低音或高音) 

如果未找到这些控件，则 SndVol32 不会显示面板。 源行只是不带控件的 MUX 的一部分，不能用于显示。 通过在拓扑中插入一个虚设的静音控件来使面板显示，可轻松规避此限制。 当行只进到 MUX 中时，为 Mux 显示的 " **选择** " 框将隐藏静音控件。

SndVol32 不会显示无法很好地映射到混音器线条控制的 WDM 音频拓扑节点。 有关将哪些节点转换为混音器控件的详细信息，请参阅 [拓扑节点](topology-nodes.md) 。 WDM 混音器驱动程序将一些节点转换为控件，但 SndVol32 只显示它知道的一组控件。

有关各个版本 Windows 中的卷范围和默认卷级别的信息，请参阅 [默认音频音量设置](default-audio-volume-settings.md)。

 

 




