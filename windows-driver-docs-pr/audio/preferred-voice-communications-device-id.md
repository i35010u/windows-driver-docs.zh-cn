---
title: 首选的语音通信设备 ID
description: 首选的语音通信设备 ID
ms.assetid: ed0fbba3-cc9e-48d6-9ab5-360f8aab3ed6
keywords:
- WDM 音频扩展 WDK，语音通信设备 Id
- 语音通信设备 Id WDK 音频
- 设备 Id WDK 音频
- 识别的音频设备
- 首选的设备 Id WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fb5b8b04d2bf243e2d3b3b181e5d45b54d05b7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328751"
---
# <a name="preferred-voice-communications-device-id"></a>首选的语音通信设备 ID


## <span id="preferred_voice_communications_device_id"></span><span id="PREFERRED_VOICE_COMMUNICATIONS_DEVICE_ID"></span>


在 Windows Me 和 Windows 2000 和更高版本、 Windows 多媒体函数**waveInMessage**并**waveOutMessage**可以检索适用于语音通信的首选设备的设备 ID。 这两个函数获取首选的语音通信设备 Id 的批输入和 wave 输出分别。 每个设备 ID 用于标识是专门为语音通信，与常规波形音频的使用情况的首选的波形设备相比首选波形设备。 有关获取适用于常规波形音频的首选设备的设备 ID 的信息，请参阅[访问首选的设备 ID](accessing-the-preferred-device-id.md)。

了解首选的语音通信设备非常有帮助的例如，允许用户选择要打开的两个或多个设备列表中的设备应用程序程序。 此类应用程序通常需要以指示它在列表中的设备之间是首选的设备。

若要检索当前的首选的语音通信设备的设备 ID，应用程序调用批*Xxx*消息使用消息参数设置为常量函数[ **DRVM\_映射器\_CONSOLEVOICECOM\_获取**](https://msdn.microsoft.com/library/windows/hardware/ff536361)。

调用时**waveInMessage**或**waveOutMessage**函数和 DRVM\_映射器\_CONSOLEVOICECOM\_收到消息，指定设备的值作为批进行处理\_映射器并将此值设置为相应的句柄类型，HWAVEIN 或 HWAVEOUT 强制转换。 Wave *Xxx*函数接受此值来替换有效的设备句柄，以便应用程序可查询的默认设备 ID，而不必首先打开设备的消息。 有关批的详细信息*Xxx*消息的函数，请参见[System-Intercepted 设备的消息](system-intercepted-device-messages.md)。

DRVM\_映射器\_首选\_GET 消息截获 （waveIn 或 waveOut） 的目标设备映射器。 有关适用于批设备映射器的信息，请参阅 Microsoft Windows SDK 文档。

 

 




