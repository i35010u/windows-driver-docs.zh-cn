---
title: DirectMusic 用户模式合成器和合成器接收器接口
description: DirectMusic 用户模式合成器和合成器接收器接口
ms.assetid: 2b25f605-d9e6-415e-8f45-08f7cdd2f625
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 300de362dd4b7c01131403ceec710f040d8c888f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714794"
---
# <a name="directmusic-user-mode-synth-and-synth-sink-interfaces"></a>DirectMusic 用户模式合成器和合成器接收器接口


## <span id="ddk_directmusic_user_mode_synth_and_synth_sink_interfaces_ks"></span><span id="DDK_DIRECTMUSIC_USER_MODE_SYNTH_AND_SYNTH_SINK_INTERFACES_KS"></span>


本部分介绍 synths 和合成接收器的 DirectMusic 用户模式接口。 如 [用户模式和内核模式](./user-mode-versus-kernel-mode.md)中所述，这些接口可用于开发用户模式下的驱动程序代码，以后可将其移植到内核模式。 有关信息，请参阅 [合成和波形接收器](./synthesizers-and-wave-sinks.md)。

本部分提供了以下两个用户模式接口：

用户模式合成接口

用户模式合成接收器的接口

[IDirectMusicSynth](/windows/win32/api/dmusics/nn-dmusics-idirectmusicsynth)

[IDirectMusicSynthSink](/windows/win32/api/dmusics/nn-dmusics-idirectmusicsynthsink)

 

