---
title: MIDI 的音频设备消息
description: MIDI 的音频设备消息
ms.assetid: d3b00985-6894-41ea-b493-d0aee269d5bf
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f082a76f1ffad1eb4993aed573b58d99769fd62a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355739"
---
# <a name="audio-device-messages-for-midi"></a>MIDI 的音频设备消息


在 Windows XP 和更高版本的 Windows （包括 Windows Vista），操作系统与通信乐器数字接口 (MIDI) 输入和输出的驱动程序通过使用音频设备的消息。

每个 MIDI 输入和输出驱动程序必须具有一个[DriverProc](https://go.microsoft.com/fwlink/p/?linkid=142258)入口点函数来启用或禁用驱动程序。 此外，它必须从 Windows 操作系统处理的消息具有其他入口点函数。 在 MIDI 输出驱动程序的情况下是其他入口点函数[ **modMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537532(v=vs.85))，这必须通过 MIDI 设备制造商提供。 此函数将处理 WINMM 向 MIDI 输出驱动程序发送的消息。 WINMM 是包含函数，用于帮助操作系统和 MIDI 输出驱动程序与彼此通信的 Windows 动态链接库 (DLL) 模块。 具体而言，WINMM 有助于管理在 Windows 运行的 16 位多媒体应用程序。

收到的每条消息**modMessage**函数随附了两个指针 DWORD 变量 (DWORD\_PTR)。 对于某些消息，其中一个参数指向一个结构，包含其他信息从客户端，或它指向一个空的结构的驱动程序以使用客户端的信息填充。 此类结构的一个示例是[ **MIDIOPENDESC**](https://docs.microsoft.com/windows/desktop/api/mmddk/ns-mmddk-midiopendesc_tag)。 有两个 MIDI 输出设备驱动程序使用其他结构和 Windows SDK 中讨论。 有关这些结构的详细信息，请参阅[MIDIHDR](https://go.microsoft.com/fwlink/p/?linkid=142406)并[MIDIOUTCAPS](https://go.microsoft.com/fwlink/p/?linkid=142347)。

以下是音频设备的消息的列表和**modMessage**入口点 MIDI 输出驱动程序对其进行处理的函数：

[**modMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537532(v=vs.85))

[**MODM\_CACHEDRUMPATCHES**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537533(v=vs.85))

[**MODM\_CACHEPATCHES**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537534(v=vs.85))

[**MODM\_DATA**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537535(v=vs.85))

[**MODM\_GETDEVCAPS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537536(v=vs.85))

[**MODM\_GETNUMDEVS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537537(v=vs.85))

[**MODM\_GETPOS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537538(v=vs.85))

[**MODM\_GETVOLUME**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537539(v=vs.85))

[**MODM\_LONGDATA**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537540(v=vs.85))

[**MODM\_OPEN**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537541(v=vs.85))

[**MODM\_PAUSE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537542(v=vs.85))

[**MODM\_PREPARE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537543(v=vs.85))

[**MODM\_PROPERTIES**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537544(v=vs.85))

[**MODM\_RESET**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537545(v=vs.85))

[**MODM\_RESTART**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537546(v=vs.85))

[**MODM\_SETVOLUME**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537547(v=vs.85))

[**MODM\_STOP**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537548(v=vs.85))

[**MODM\_STRMDATA**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537549(v=vs.85))

[**MODM\_UNPREPARE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537550(v=vs.85))

[**MOM\_CLOSE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537551(v=vs.85))

[**MOM\_完成**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537552(v=vs.85))

[**MOM\_打开**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537553(v=vs.85))

 

 





