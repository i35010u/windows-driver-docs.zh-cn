---
title: 访问首选的设备 ID
description: 访问首选的设备 ID
ms.assetid: ef964ce5-8bcc-4ab0-9522-b05a8a6bdf74
keywords:
- 首选设备 Id WDK 音频
- WDM 音频扩展 WDK，首选设备 Id
- 设备 Id WDK 音频
- 识别音频设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b11c8e9a06d98a78affcfbe87de5c00d2bcaee12
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208383"
---
# <a name="accessing-the-preferred-device-id"></a>访问首选的设备 ID


## <span id="accessing_the_preferred_device_id"></span><span id="ACCESSING_THE_PREFERRED_DEVICE_ID"></span>


在 Windows Me 和 Windows 2000 及更高版本中，Windows 多媒体函数 **waveInMessage**、 **waveOutMessage**和 **midiOutMessage** 可以检索首选设备的设备 ID。 这三个函数分别为波输入、波形输出和 MIDI 输出获取首选设备 Id。 此信息对应用程序非常有用，例如，允许用户从两个或更多设备的列表中选择要打开的设备。 此类应用程序通常需要指明列表中的设备是首选设备。

首选设备是用户通过多媒体控制面板选择的设备，mmsys.cpl。 如果 Windows 多媒体或 DirectSound 应用程序未显式指定设备，则默认情况下将选择首选设备。

若要检索当前首选音频设备的设备 ID，应用程序将调用 *xxx * * * message** 函数，并将 message 参数设置为常量 [**DRVM 映射 \_ 器 \_ 首选 \_ GET**](/previous-versions/windows/hardware/drivers/ff536362(v=vs.85))。

当调用**waveInMessage**、 **waveOutMessage**或**midiOutMessage**函数与 DRVM \_ 映射器 \_ 首选 \_ GET 消息时，请将设备句柄的值指定为 waveInMessage \_ 或**waveOutMessage**) **waveInMessage** () 的波形映射器 (， \_ 并**midiOutMessage**将此值转换为相应的句柄类型： midiOutMessage、HWAVEIN 或 HWAVEOUT。 *Xxx * * * Message** 函数接受此值来代替有效的设备句柄，以便应用程序无需首先打开设备即可查询默认设备 ID。 有关 *xxx * * * Message** 函数的详细信息，请参阅 [系统截获的设备消息](system-intercepted-device-messages.md)。

DRVM \_ 映射器 \_ 首选 \_ GET 消息由目标设备的映射器截获 (waveIn、waveOut 或 midiOut) 。 有关 wave 和 MIDI 设备的映射器的信息，请参阅 Microsoft Windows SDK 文档。

 

