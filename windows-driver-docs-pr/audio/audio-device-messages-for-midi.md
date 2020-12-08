---
title: MIDI 的音频设备消息
description: MIDI 的音频设备消息
ms.date: 04/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: a778a68f3d28c84b6e0dfa216b22c7a0c0a6cea2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785009"
---
# <a name="audio-device-messages-for-midi"></a>MIDI 的音频设备消息


在 windows XP 和更高版本的 Windows (包括 Windows Vista) 中，操作系统使用音频设备消息与乐器 (MIDI) 输入和输出驱动程序通信。

每个 MIDI 输入和输出驱动程序都必须有一个 [DriverProc](/windows/win32/api/mmiscapi/nc-mmiscapi-driverproc) 入口点函数，以启用或禁用该驱动程序。 此外，它还必须具有用于处理 Windows 操作系统消息的附加入口点函数。 对于 MIDI 输出驱动程序，附加入口点函数是 [**modMessage**](/previous-versions/windows/hardware/drivers/ff537532(v=vs.85))，它必须由 MIDI 设备的制造商提供。 此函数处理 WINMM.DLL 发送到 MIDI 输出驱动程序的消息。 WINMM.DLL 是一个 Windows 动态链接库 (DLL) 模块，其中包含的功能可帮助操作系统和 MIDI 输出驱动程序相互通信。 具体而言，WINMM.DLL 可帮助管理在 Windows 上运行的16位多媒体应用程序。

**ModMessage** 函数收到的每条消息都带有两个指向 dword 变量 (指针 \_) 的 dword PTR。 对于某些消息，其中一个参数指向包含来自客户端的其他信息的结构，或指向用于填写客户端信息的驱动程序的空结构。 这种结构的一个示例是 [**MIDIOPENDESC**](/windows/win32/api/mmddk/ns-mmddk-midiopendesc)。 MIDI 输出设备驱动程序使用另外两个结构，Windows SDK 中对它们进行了讨论。 有关这些结构的详细信息，请参阅 [MIDIHDR](/windows/win32/api/mmeapi/ns-mmeapi-midihdr) 和 [MIDIOUTCAPS](/windows/win32/api/mmeapi/ns-mmeapi-midioutcaps)。

下面列出了音频设备消息和用于处理 MIDI 输出驱动程序的 **modMessage** 入口点函数：

[**modMessage**](/previous-versions/windows/hardware/drivers/ff537532(v=vs.85))

[**MODM \_ CACHEDRUMPATCHES**](/previous-versions/windows/hardware/drivers/ff537533(v=vs.85))

[**MODM \_ CACHEPATCHES**](/previous-versions/windows/hardware/drivers/ff537534(v=vs.85))

[**MODM \_ 数据**](/previous-versions/windows/hardware/drivers/ff537535(v=vs.85))

[**MODM \_ GETDEVCAPS**](/previous-versions/windows/hardware/drivers/ff537536(v=vs.85))

[**MODM \_ GETNUMDEVS**](/previous-versions/windows/hardware/drivers/ff537537(v=vs.85))

[**MODM \_ GETPOS**](/previous-versions/windows/hardware/drivers/ff537538(v=vs.85))

[**MODM \_ GETVOLUME**](/previous-versions/windows/hardware/drivers/ff537539(v=vs.85))

[**MODM \_ LONGDATA**](/previous-versions/windows/hardware/drivers/ff537540(v=vs.85))

[**MODM \_ 打开**](/previous-versions/windows/hardware/drivers/ff537541(v=vs.85))

[**MODM \_ 暂停**](/previous-versions/windows/hardware/drivers/ff537542(v=vs.85))

[**MODM \_ 准备**](/previous-versions/windows/hardware/drivers/ff537543(v=vs.85))

[**MODM \_ 属性**](/previous-versions/windows/hardware/drivers/ff537544(v=vs.85))

[**MODM \_ 重置**](/previous-versions/windows/hardware/drivers/ff537545(v=vs.85))

[**MODM \_ 重新启动**](/previous-versions/windows/hardware/drivers/ff537546(v=vs.85))

[**MODM \_ SETVOLUME**](/previous-versions/windows/hardware/drivers/ff537547(v=vs.85))

[**MODM \_ 停止**](/previous-versions/windows/hardware/drivers/ff537548(v=vs.85))

[**MODM \_ STRMDATA**](/previous-versions/windows/hardware/drivers/ff537549(v=vs.85))

[**MODM \_ UNPREPARE**](/previous-versions/windows/hardware/drivers/ff537550(v=vs.85))

[**MOM \_ 关闭**](/previous-versions/windows/hardware/drivers/ff537551(v=vs.85))

[**MOM \_ 完成**](/previous-versions/windows/hardware/drivers/ff537552(v=vs.85))

[**MOM \_ 打开**](/previous-versions/windows/hardware/drivers/ff537553(v=vs.85))

 

