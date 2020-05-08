---
title: MIDI 的音频设备消息
description: MIDI 的音频设备消息
ms.assetid: d3b00985-6894-41ea-b493-d0aee269d5bf
ms.date: 04/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: c86b7310e067ddc867ae01fa710a9f5ef60f9563
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925504"
---
# <a name="audio-device-messages-for-midi"></a>MIDI 的音频设备消息


在 windows XP 和更高版本的 Windows （包括 Windows Vista）中，操作系统使用音频设备消息与乐器数字接口（MIDI）输入和输出驱动程序通信。

每个 MIDI 输入和输出驱动程序都必须有一个[DriverProc](https://docs.microsoft.com/windows/win32/api/mmiscapi/nc-mmiscapi-driverproc)入口点函数，以启用或禁用该驱动程序。 此外，它还必须具有用于处理 Windows 操作系统消息的附加入口点函数。 对于 MIDI 输出驱动程序，附加入口点函数是[**modMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537532(v=vs.85))，它必须由 MIDI 设备的制造商提供。 此函数处理 WINMM.DLL 发送到 MIDI 输出驱动程序的消息。 WINMM.DLL 是一个 Windows 动态链接库（DLL）模块，其中包含的功能可帮助操作系统和 MIDI 输出驱动程序相互通信。 具体而言，WINMM.DLL 可帮助管理在 Windows 上运行的16位多媒体应用程序。

**ModMessage**函数收到的每条消息都带有两个指向 dword 变量（dword\_PTR）的指针。 对于某些消息，其中一个参数指向包含来自客户端的其他信息的结构，或指向用于填写客户端信息的驱动程序的空结构。 这种结构的一个示例是[**MIDIOPENDESC**](https://docs.microsoft.com/windows/desktop/api/mmddk/ns-mmddk-midiopendesc_tag)。 MIDI 输出设备驱动程序使用另外两个结构，Windows SDK 中对它们进行了讨论。 有关这些结构的详细信息，请参阅[MIDIHDR](https://docs.microsoft.com/windows/win32/api/mmeapi/ns-mmeapi-midihdr)和[MIDIOUTCAPS](https://docs.microsoft.com/windows/win32/api/mmeapi/ns-mmeapi-midioutcaps)。

下面列出了音频设备消息和用于处理 MIDI 输出驱动程序的**modMessage**入口点函数：

[**modMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537532(v=vs.85))

[**MODM\_CACHEDRUMPATCHES**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537533(v=vs.85))

[**MODM\_CACHEPATCHES**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537534(v=vs.85))

[**MODM\_数据**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537535(v=vs.85))

[**MODM\_GETDEVCAPS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537536(v=vs.85))

[**MODM\_GETNUMDEVS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537537(v=vs.85))

[**MODM\_GETPOS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537538(v=vs.85))

[**MODM\_GETVOLUME**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537539(v=vs.85))

[**MODM\_LONGDATA**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537540(v=vs.85))

[**MODM\_打开**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537541(v=vs.85))

[**MODM\_暂停**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537542(v=vs.85))

[**MODM\_准备**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537543(v=vs.85))

[**MODM\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537544(v=vs.85))

[**MODM\_重置**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537545(v=vs.85))

[**MODM\_重新启动**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537546(v=vs.85))

[**MODM\_SETVOLUME**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537547(v=vs.85))

[**MODM\_停止**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537548(v=vs.85))

[**MODM\_STRMDATA**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537549(v=vs.85))

[**MODM\_UNPREPARE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537550(v=vs.85))

[**MOM\_关闭**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537551(v=vs.85))

[**MOM\_完成**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537552(v=vs.85))

[**MOM\_打开**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537553(v=vs.85))

 

 





