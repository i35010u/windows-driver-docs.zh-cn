---
title: 系统截获的设备消息
description: 系统截获的设备消息
ms.assetid: 5cf1c9a6-e56f-4358-933f-e8aa2ad1b1da
keywords:
- 向旧设备发送的设备消息 WDK 音频
- WDM 音频扩展 WDK，系统拦截的设备消息
- 系统拦截的设备消息 WDK 音频
- 消息 WDK 音频
- 截获的设备消息 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66330a6b3cb4a8d4bfae7005591e6adb9af4a8ae
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210337"
---
# <a name="system-intercepted-device-messages"></a>系统截获的设备消息


## <span id="system_intercepted_device_messages"></span><span id="SYSTEM_INTERCEPTED_DEVICE_MESSAGES"></span>


以下 Windows 多媒体函数提供了一种方法，供调用方将消息传递到旧版音频设备：

-   [**waveInMessage**](/previous-versions/dd743846(v=vs.85))

-   [**waveOutMessage**](/previous-versions/dd743865(v=vs.85))

-   [**midiInMessage**](/previous-versions/dd798457(v=vs.85))

-   [**midiOutMessage**](/previous-versions/dd798475(v=vs.85))

-   [**mixerMessage**](/previous-versions/dd757307(v=vs.85))

-   [**auxOutMessage**](/previous-versions/dd756716(v=vs.85))

其中一些设备消息由设备驱动程序直接处理，一些则由系统代表设备进行处理。

本部分只讨论系统拦截的消息，并在不传递到设备驱动程序的情况下进行处理。 系统拦截的消息可以获得用于语音通信的首选设备或一般音频使用情况。 此外，系统拦截的消息可提供有关特定设备的下列信息：

-   **设备接口名称**

    有关设备接口名称的信息，请参阅 [设备接口简介](../install/overview-of-device-interface-classes.md)。

-   **设备的即插即用 devnode 号**

    有关 devnodes 的信息，请参阅 [设备树](../kernel/device-tree.md)。

-   **映射器是否可以使用设备**

    映射器通过将应用程序的要求映射到系统中的一个可用设备来选择相应的设备。 有关映射器的详细信息，请参阅 Microsoft Windows SDK 文档。

有关其他类型的设备消息的信息，请参阅 Windows SDK 文档。

*Xxx*消息函数具有以下语法：

```cpp
DWORD XxxMessage(
<device ID>,
    UINT  uMsg,
    DWORD_PTR  dwParam1,
    DWORD_PTR  dwParam2
    );
```

第一个参数是设备 ID。 [**AuxOutMessage**](/previous-versions/dd756716(v=vs.85))函数定义将此参数指定为 UINT 类型（如预期）。 但对于 [**waveInMessage**](/previous-versions/dd743846(v=vs.85))、 [**waveOutMessage**](/previous-versions/dd743865(v=vs.85))、 [**midiInMessage**](/previous-versions/dd798457(v=vs.85))、 [**midiOutMessage**](/previous-versions/dd798475(v=vs.85))或 [**mixerMessage**](/previous-versions/dd757307(v=vs.85))，调用方必须将设备 ID 强制转换为分别处理类型 HWAVEIN、HWAVEOUT、HMIDIIN、HMIDIOUT 或 HMIXER。 请注意，如果调用方为此参数提供有效的句柄而不是设备 ID，则该函数将失败并返回错误代码 MMSYSERR \_ NOSUPPORT。

*UMsg*参数指定消息值 (例如， [**winspool.drv \_ QUERYDEVICEINTERFACE**](/previous-versions/windows/hardware/drivers/ff536363(v=vs.85))) 。 有关驱动程序特定消息的列表，请参阅头文件 Mmddk。

参数 *dwParam1* 和 *dwParam2* 的含义取决于消息。 例如，特定消息可能要求 *dwParam1* 是 ULONG 值;调用方必须将此值转换为类型 DWORD \_ PTR 才能满足函数定义。

\_如果调用成功，则函数返回 MMERR NOERROR; 如果不是，则返回错误状态代码。

有关 *Xxx*消息函数的详细信息，请参阅 Windows SDK 文档。

标头文件 Mmddk 定义以下系统截获的设备消息：

[**WINSPOOL.DRV \_ QUERYDEVICEINTERFACE**](/previous-versions/windows/hardware/drivers/ff536363(v=vs.85))

有关详细信息，请参阅 [获取设备接口名称](obtaining-a-device-interface-name.md)。

[**WINSPOOL.DRV \_ QUERYDEVICEINTERFACESIZE**](/previous-versions/windows/hardware/drivers/ff536364(v=vs.85))

有关详细信息，请参阅 **获取设备接口名称**。

[**WINSPOOL.DRV \_ QUERYDEVNODE**](/previous-versions/windows/hardware/drivers/ff536365(v=vs.85))

查询设备的 devnode 编号。

[**WINSPOOL.DRV \_ QUERYMAPPABLE**](/previous-versions/windows/hardware/drivers/ff536366(v=vs.85))

查询映射器是否可以使用设备。

[**DRVM \_ 映射器 \_ CONSOLEVOICECOM \_ 获取**](/previous-versions/windows/hardware/drivers/ff536361(v=vs.85))

有关详细信息，请参阅 [首选语音通信设备 ID](preferred-voice-communications-device-id.md)。

[**DRVM \_ 映射器 \_ 首选 \_ GET**](/previous-versions/windows/hardware/drivers/ff536362(v=vs.85))

有关详细信息，请参阅 [访问首选设备 ID](accessing-the-preferred-device-id.md)。

 

