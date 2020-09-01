---
title: 首选的语音通信设备 ID
description: 首选的语音通信设备 ID
ms.assetid: ed0fbba3-cc9e-48d6-9ab5-360f8aab3ed6
keywords:
- WDM 音频扩展 WDK，语音通信设备 Id
- 语音通信设备 Id WDK 音频
- 设备 Id WDK 音频
- 识别音频设备
- 首选设备 Id WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdbcfbbd01de6ce1429b34444107d7178aa9c5bc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210455"
---
# <a name="preferred-voice-communications-device-id"></a>首选的语音通信设备 ID


## <span id="preferred_voice_communications_device_id"></span><span id="PREFERRED_VOICE_COMMUNICATIONS_DEVICE_ID"></span>


在 Windows Me 和 Windows 2000 及更高版本中，Windows 多媒体函数 **waveInMessage** 和 **waveOutMessage** 可以检索语音通信的首选设备的设备 ID。 这两个函数分别为波输入和波形输出获取首选的语音通信设备 Id。 每个设备 ID 都标识专用于语音通信的声波设备，这与一般波形音频用量首选的 wave 设备不同。 有关为常规波形音频获取首选设备的设备 ID 的信息，请参阅 [访问首选设备 id](accessing-the-preferred-device-id.md)。

了解首选语音通信设备对应用程序很有帮助，例如，允许用户从两个或更多设备的列表中选择要打开的设备。 此类应用程序通常需要指明列表中的设备是首选设备。

若要检索当前首选语音通信设备的设备 ID，应用程序将调用波 *Xxx*消息函数，并将 message 参数设置为常量 [**DRVM 映射器 \_ \_ CONSOLEVOICECOM \_ GET**](/previous-versions/windows/hardware/drivers/ff536361(v=vs.85))。

当通过 DRVM 映射器 CONSOLEVOICECOM GET 消息调用 **waveInMessage** 或 **waveOutMessage** 函数时 \_ \_ \_ ，请将设备句柄的值指定为波形映射器， \_ 并将此值转换为相应的句柄类型 HWAVEIN 或 HWAVEOUT。 波浪 *Xxx*消息函数接受此值来代替有效的设备句柄，以便应用程序无需首先打开设备即可查询默认设备 ID。 有关波浪 *Xxx*消息函数的详细信息，请参阅 [系统拦截的设备消息](system-intercepted-device-messages.md)。

DRVM \_ 映射器 \_ 首选 \_ GET 消息被目标设备的映射器截获 (waveIn 或 waveOut) 。 有关 wave 设备的映射器的信息，请参阅 Microsoft Windows SDK 文档。

 

