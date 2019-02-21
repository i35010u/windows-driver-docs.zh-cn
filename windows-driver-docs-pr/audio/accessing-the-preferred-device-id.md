---
title: 访问首选的设备 ID
description: 访问首选的设备 ID
ms.assetid: ef964ce5-8bcc-4ab0-9522-b05a8a6bdf74
keywords:
- 首选的设备 Id WDK 音频
- WDM 音频扩展 WDK，首选设备 Id
- 设备 Id WDK 音频
- 识别的音频设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12d98ddd9a95352e165b33d529ba389ef139cdf4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522427"
---
# <a name="accessing-the-preferred-device-id"></a>访问首选的设备 ID


## <span id="accessing_the_preferred_device_id"></span><span id="ACCESSING_THE_PREFERRED_DEVICE_ID"></span>


在 Windows Me 和 Windows 2000 和更高版本、 Windows 多媒体函数**waveInMessage**， **waveOutMessage**，并**midiOutMessage**可以检索的设备 ID首选的设备。 这三个函数分别获取批输入、 批输出和 MIDI 输出的首选的设备 Id。 此信息可为应用程序的程序，例如，允许用户选择要打开的两个或多个设备列表中的设备。 此类应用程序通常需要以指示它在列表中的设备之间是首选的设备。

首选的设备是用户通过多媒体控件面板中，选择设备 mmsys.cpl。 如果 Windows 多媒体或 DirectSound 应用程序未显式指定设备，默认情况下选择首选的设备。

若要检索当前的首选音频设备的设备 ID，应用程序调用*xxx * * * 消息** 函数使用消息参数设置为常量[ **DRVM\_映射器\_首选\_获取**](https://msdn.microsoft.com/library/windows/hardware/ff536362)。

调用时**waveInMessage**， **waveOutMessage**，或**midiOutMessage**配合 DRVM\_映射器\_首选\_收到消息，设备句柄的值指定为批\_映射器 (对于**waveInMessage**或**waveOutMessage**) 或 MIDI\_映射器 (对于**midiOutMessage**) 并将此值设置为相应的句柄类型强制转换：HWAVEIN、 HWAVEOUT 或 HMIDIOUT。 *Xxx * * * 消息** 函数接受此值来替换有效的设备句柄，以便应用程序可查询的默认设备 ID，而不必首先打开设备。 有关详细信息*xxx * * * 消息** 函数，请参阅[System-Intercepted 设备的消息](system-intercepted-device-messages.md)。

DRVM\_映射器\_首选\_GET 消息截获 （waveIn、 waveOut 或 midiOut） 的目标设备映射器。 有关批和 MIDI 设备映射器的信息，请参阅 Microsoft Windows SDK 文档。

 

 




