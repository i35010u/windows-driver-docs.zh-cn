---
title: MIDI 的音频设备消息
description: MIDI 的音频设备消息
ms.assetid: d3b00985-6894-41ea-b493-d0aee269d5bf
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4f537882be7a29213af1b2320e6fb48aac4ec6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566828"
---
# <a name="audio-device-messages-for-midi"></a>MIDI 的音频设备消息


在 Windows XP 和更高版本的 Windows （包括 Windows Vista），操作系统与通信乐器数字接口 (MIDI) 输入和输出的驱动程序通过使用音频设备的消息。

每个 MIDI 输入和输出驱动程序必须具有一个[DriverProc](https://go.microsoft.com/fwlink/p/?linkid=142258)入口点函数来启用或禁用驱动程序。 此外，它必须从 Windows 操作系统处理的消息具有其他入口点函数。 在 MIDI 输出驱动程序的情况下是其他入口点函数[ **modMessage**](https://msdn.microsoft.com/library/windows/hardware/ff537532)，这必须通过 MIDI 设备制造商提供。 此函数将处理 WINMM 向 MIDI 输出驱动程序发送的消息。 WINMM 是包含函数，用于帮助操作系统和 MIDI 输出驱动程序与彼此通信的 Windows 动态链接库 (DLL) 模块。 具体而言，WINMM 有助于管理在 Windows 运行的 16 位多媒体应用程序。

收到的每条消息**modMessage**函数随附了两个指针 DWORD 变量 (DWORD\_PTR)。 对于某些消息，其中一个参数指向一个结构，包含其他信息从客户端，或它指向一个空的结构的驱动程序以使用客户端的信息填充。 此类结构的一个示例是[ **MIDIOPENDESC**](https://msdn.microsoft.com/library/windows/hardware/ff537518)。 有两个 MIDI 输出设备驱动程序使用其他结构和 Windows SDK 中讨论。 有关这些结构的详细信息，请参阅[MIDIHDR](https://go.microsoft.com/fwlink/p/?linkid=142406)并[MIDIOUTCAPS](https://go.microsoft.com/fwlink/p/?linkid=142347)。

以下是音频设备的消息的列表和**modMessage**入口点 MIDI 输出驱动程序对其进行处理的函数：

[**modMessage**](https://msdn.microsoft.com/library/windows/hardware/ff537532)

[**MODM\_CACHEDRUMPATCHES**](https://msdn.microsoft.com/library/windows/hardware/ff537533)

[**MODM\_CACHEPATCHES**](https://msdn.microsoft.com/library/windows/hardware/ff537534)

[**MODM\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff537535)

[**MODM\_GETDEVCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff537536)

[**MODM\_GETNUMDEVS**](https://msdn.microsoft.com/library/windows/hardware/ff537537)

[**MODM\_GETPOS**](https://msdn.microsoft.com/library/windows/hardware/ff537538)

[**MODM\_GETVOLUME**](https://msdn.microsoft.com/library/windows/hardware/ff537539)

[**MODM\_LONGDATA**](https://msdn.microsoft.com/library/windows/hardware/ff537540)

[**MODM\_OPEN**](https://msdn.microsoft.com/library/windows/hardware/ff537541)

[**MODM\_PAUSE**](https://msdn.microsoft.com/library/windows/hardware/ff537542)

[**MODM\_PREPARE**](https://msdn.microsoft.com/library/windows/hardware/ff537543)

[**MODM\_PROPERTIES**](https://msdn.microsoft.com/library/windows/hardware/ff537544)

[**MODM\_RESET**](https://msdn.microsoft.com/library/windows/hardware/ff537545)

[**MODM\_RESTART**](https://msdn.microsoft.com/library/windows/hardware/ff537546)

[**MODM\_SETVOLUME**](https://msdn.microsoft.com/library/windows/hardware/ff537547)

[**MODM\_STOP**](https://msdn.microsoft.com/library/windows/hardware/ff537548)

[**MODM\_STRMDATA**](https://msdn.microsoft.com/library/windows/hardware/ff537549)

[**MODM\_UNPREPARE**](https://msdn.microsoft.com/library/windows/hardware/ff537550)

[**MOM\_CLOSE**](https://msdn.microsoft.com/library/windows/hardware/ff537551)

[**MOM\_完成**](https://msdn.microsoft.com/library/windows/hardware/ff537552)

[**MOM\_打开**](https://msdn.microsoft.com/library/windows/hardware/ff537553)

 

 





