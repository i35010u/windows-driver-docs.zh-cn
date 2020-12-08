---
title: 将合成器作为旧设备公开
description: 将合成器作为旧设备公开
keywords:
- 合成 WDK 音频，旧设备
- 旧设备支持 WDK DirectMusic
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e9869e9e09d678c87d515df72de2aa357b4d9c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786547"
---
# <a name="exposing-your-synthesizer-as-a-legacy-device"></a>将合成器作为旧设备公开


## <span id="exposing_your_synthesizer_as_a_legacy_device"></span><span id="EXPOSING_YOUR_SYNTHESIZER_AS_A_LEGACY_DEVICE"></span>


你可能需要编写一个设备驱动程序，该驱动程序通过 Windows 多媒体 midiOut *Xxx* API) ，将合成硬件公开为 DirectMusic 设备和传统的 MIDI 设备 (。 此方法在以下三种情况下非常有用：

1.  如果设备不支持 DLS，则为。 示例包括 MPU-401 驱动程序 (参阅 Windows 驱动程序工具包中的 mpu401 示例 \[ \]) 、仅具有 ROM 集的设备和固定功能软件合成 (例如 FM) 。

    在这种情况下，设备可以公开旧版 MIDI 接口以及 DirectMusic 接口。 它应该只公开一个旧的 MIDI pin。 首先列出与旧接口的 pin，以便 WDM 音频将其枚举为旧式 MIDI 设备，这一点非常重要。

2.  如果设备支持 DLS，但仍处于加载状态。 此设备的每个 DLS 和 ROM 都包含 GM/GS/XG wave 表。

    在这种情况下，设备还可以同时公开这两个接口。 如果这两个接口互相排斥 (即，一旦您下载了某个内容，该 ROM 就不会显示) ，然后它应该是具有两个接口的单一 pin，可选择 (而不是两个 pin) 。

3.  如果设备支持 DLS，但启动了 "empty" (例如，DirectMusic software 合成) ，因此需要通过 DLS 下载来初始化其波形表。

    如果设备在 ROM 中具有默认示例集时不需要使用 DLS 下载，则不需要进行此初始化 (例如) 或打开 DirectMusic pin (DirectMusic Api 确保 DL 下载) 。

    通过旧版 Api 公开你的 DLS 设备需要额外的工作。 当在需要 DLS 设备的设备上打开旧版 pin 时，驱动程序应找到并打开一个文件，其中包含要使用的 DLS 集合。 然后，该驱动程序应拦截更新和银行更改，从 DLS 文件中检索相应的数据，并对设备执行必要的 DL 下载。

    这种情况有问题，因为 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver) 和其他客户端并不知道他们需要下载集合。 它们只是开始发送 MIDI 更新更改和说明。

 

 




