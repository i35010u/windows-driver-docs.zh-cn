---
title: 将你合成器公开为旧设备
description: 将你合成器公开为旧设备
ms.assetid: 25e5e14f-1db5-45dc-9048-674420d79824
keywords:
- 合成器 WDK 音频的旧设备
- 旧的设备支持 WDK DirectMusic
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40b7a6c4b531f921215d419f8053f43e6f8c4e22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533183"
---
# <a name="exposing-your-synthesizer-as-a-legacy-device"></a>将你合成器公开为旧设备


## <span id="exposing_your_synthesizer_as_a_legacy_device"></span><span id="EXPOSING_YOUR_SYNTHESIZER_AS_A_LEGACY_DEVICE"></span>


你可能想要编写将合成器硬件公开为 DirectMusic 设备而旧的 MIDI 设备的单个设备驱动程序 (即，通过 Windows 多媒体 midiOut*Xxx* API)。 此方法可在以下三种情况：

1.  如果设备不支持 DLS。 示例包括 MPU 401 驱动程序 (请参阅 Windows 驱动程序工具包中的 mpu401 示例\[WDK\])，具有仅设置，ROM 的设备和固定功能软件合成器 (例如，FM)。

    在这种情况下，设备可以公开旧版 MIDI 接口，以及 DirectMusic 接口。 它应公开一个旧的 MIDI pin。 请务必首先列出 pin 与旧版的接口，以便 WDM 音频枚举它为旧的 MIDI 设备。

2.  如果设备不支持 DLS，但功能会在加载状态中。 此设备有两个 RAM DLS 和 ROM 包含 GM/GS/XG 批表。

    在这种情况下，设备还可以公开这两个接口。 如果两个接口是互斥 （即，如果一次下载内容，ROM 不可见），则它应是具有两个接口，可供选择 （而不是两个 pin) 单个插针。

3.  当设备支持 DLS，但为"空"（例如，DirectMusic 软件合成） 提供支持，而且因此需要通过 DLS 下载进程，以初始化其批表。

    此初始化是不必要的如果设备不需要 DLS 下载 （如果它没有默认示例，例如在 ROM 中设置），或打开 DirectMusic pin （DirectMusic Api 可确保出现 DLS 下载）。

    公开 DLS 设备通过旧版 Api 需要一些额外的工作。 当需要 DLS instruments 的设备上打开旧 pin 时，该驱动程序应找到并打开包含 DLS 集合要使用的文件。 该驱动程序应然后截获更新和银行更改、 从 DL 文件，检索相应的数据和执行必要的 DLS 下载到设备。

    这种情况下会产生问题由于[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)和其他客户端不知道他们需要下载一个集合。 它们只是开始发送 MIDI 更新更改和说明。

 

 




