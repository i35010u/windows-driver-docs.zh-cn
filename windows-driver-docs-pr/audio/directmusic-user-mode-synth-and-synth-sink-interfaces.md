---
title: DirectMusic 用户模式合成器和合成器接收器接口
description: DirectMusic 用户模式合成器和合成器接收器接口
ms.assetid: 2b25f605-d9e6-415e-8f45-08f7cdd2f625
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c785d71d82567de741aacc2e74edd40a90b0ba6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356546"
---
# <a name="directmusic-user-mode-synth-and-synth-sink-interfaces"></a>DirectMusic 用户模式合成器和合成器接收器接口


## <span id="ddk_directmusic_user_mode_synth_and_synth_sink_interfaces_ks"></span><span id="DDK_DIRECTMUSIC_USER_MODE_SYNTH_AND_SYNTH_SINK_INTERFACES_KS"></span>


本部分介绍 DirectMusic synths 和合成器的用户模式接口接收器。 如中所述[的用户模式下与内核模式](https://docs.microsoft.com/windows-hardware/drivers/audio/user-mode-versus-kernel-mode)，这些接口可用于开发在用户模式下的更高版本可以移植到内核模式驱动程序代码。 有关信息，请参阅[合成和批接收器](https://docs.microsoft.com/windows-hardware/drivers/audio/synthesizers-and-wave-sinks)。

本部分介绍以下两个用户模式接口：

用于用户模式下合成器的接口

中的用户模式下合成器接收器接口

[IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)

[IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)

 

 





