---
title: 系统托盘和 SndVol32
description: 系统托盘和 SndVol32
ms.assetid: 53f8c5be-d0a5-4364-8fac-813cf9f8318c
keywords:
- 系统托盘 WDK 音频
- SndVol32 WDK 音频
- 主音量设置 WDK 音频
- 扬声器 WDK 音频图标显示
- 卷设置 WDK 音频
- 图标 WDK 音频
- 显示扬声器图标
- 卷滑块 WDK 音频
- 隐藏的扬声器图标 WDK 音频
- 使控件 WDK 音频静音
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c133bebc25bc2209b8b77dfacbadac7cee0f8b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544648"
---
# <a name="systray-and-sndvol32"></a>系统托盘和 SndVol32


## <span id="systray_and_sndvol32"></span><span id="SYSTRAY_AND_SNDVOL32"></span>


SndVol32 程序 (Sndvol32.exe) 控制各种声音源 （如批、 CD、 和合成器） 的音量设置以及主音量设置。 SndVol32 程序表示为在系统任务栏通知区域显示任务栏，默认情况下，将显示 Windows 屏幕的右下角的扬声器图标。

系统托盘程序 (Systray.exe) 是负责在打开时显示的扬声器图标，并当它处于关闭状态时隐藏的扬声器图标。 在 Windows XP 中，默认情况下隐藏的扬声器图标。 在所有其他 Windows 版本，包括 Windows XP SP1 中的扬声器图标是默认情况下可见。

在 Windows XP 中，请执行以下步骤在任务栏上显示的扬声器图标：

1.  在控制面板中，单击**声音和音频设备**图标 （或只需运行的 mmsys.cpl）。

2.  上**卷**选项卡上，选择**放置在任务栏中的音量图标**复选框。

如果您的声卡的音量级别可以更改软件控制下扬声器图标出现在任务栏上。 你可以通过右键单击该图标上和调整音量滑块来设置主机卷。

在登录时，系统托盘查询音频驱动程序的一个混音器行，其中 MIXERLINE\_COMPONENTTYPE\_DST\_发言人 （演讲者目标） 或 MIXERLINE\_COMPONENTTYPE\_DST\_耳机 （耳机目标） 组件类型，以确定是否应显示的扬声器图标。 如果这些组件类型均未找到，任务栏不显示的扬声器图标。 如果找到行，它将查询用于确定它是否包含静音控件的行。 系统托盘完成处理通过在内部存储其登录时间 mixer 行**行 ID**并**静音控件 ID**以供将来参考。

SndVol32 计划还提供用于控制系统中的卷的所有控件的用户界面。 当用户双击系统任务栏中的扬声器图标 （或只需运行 Sndvol32.exe） 时，SndVol32 显示一个"主音量"窗口，其中包含用于控制主音量级别和各种声音源上的卷级别的滑块。 在这种情况下，SndVol32 使用不同的算法来确定它的显示内容。 有关**主音量滑块**，它会查找第一个卷控件上"主"目标 （例如，为带编号的零的目标）。 这通常是演讲者目标。

SndVol32 运行时，它将查询寻找一组控件，它了解 mixer 行驱动程序。 若要显示滑块面板，源行应具有至少一个以下控件：

-   音量控制

-   静音控件

-   高级控制 (AGC，低音或高音)

如果没有这些控件发现对象，SndVol32 不显示在面板。 在源行只是没有控件 MUX 的一部分是不够的显示。 通过插入假静音轻松地避开此限制到拓扑，以获取要显示的面板的控件。 当行只是馈入 MUX**选择**框显示为多路复用器隐藏了静音控件。

WDM 音频拓扑节点未映射到 mixer 行控件也不会显示通过 SndVol32。 请参阅[拓扑节点](topology-nodes.md)有关详细信息的节点将转换成 mixer 行控件。 WDM mixer 行驱动程序将某些节点转换到控件，但 SndVol32 显示只有它了解的控件组。

有关卷范围和各种版本的 Windows 中的默认卷级别的信息，请参阅[默认音频音量设置](default-audio-volume-settings.md)。

 

 




