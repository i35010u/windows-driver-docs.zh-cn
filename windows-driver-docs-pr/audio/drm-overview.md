---
title: DRM 概述
description: DRM 概述
ms.assetid: 81f47eca-aa8a-43c4-96c9-7446cba50d00
keywords:
- 数字权限管理 WDK 音频，有关 DRM
- 有关 DRM 的 DRM WDK 音频
- DRMK 系统驱动程序 WDK 音频
- 解密 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b39c7b3b3f7e7d1dda56ac4385f80efc4c54abd2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333724"
---
# <a name="drm-overview"></a>DRM 概述


## <span id="drm_overview"></span><span id="DRM_OVERVIEW"></span>


Microsoft Windows 2000 及更高版本，实现数字音频的 DRM 和 Windows Me / 98。 但是，仅 Microsoft Windows XP 及更高版本，和 Windows Me 中，实现在内核中的 DRM 安全。 目前，Windows 提供了 MIDI 流或 DLS 集没有 DRM 安全。

受 DRM 保护的数字内容存储在磁盘上的加密形式或其他存储媒体类型。 加密算法进行加密的内容以使其难以理解，直到它已解密。 在播放期间，内容将保持加密从磁盘读取并在内存中缓冲。 数据路径的结尾附近[DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver)(Drmk.sys) 对数据进行译码和直接向要播放的音频驱动程序源。 通过限制对其传输被破解的内容的数据路径的程度，DRMK 使内容不太容易受到未经授权的复制。

在 Windows 2000 和 Windows 98，安全漏洞，用户可以轻松地将加载路由到磁盘中加密的形式播放安全内容的恶意驱动程序。 Windows XP 及更高版本，和 Windows Me 中，仅受信任的音频驱动程序以用于播放受 DRM 保护内容，从而关闭这一漏洞。

在 Windows XP 及更高版本，和 Windows Me 中，安全内容都将保持加密时该代码遍历的音频数据路径，直到进入内核的受保护的环境。 在内核，受保护的组件对数据进行解码，并被破解的数据输送到用于播放的受信任的驱动程序。 在配置筛选器图形播放被破解的音频流，DRMK 进行身份验证关系图中它将每个 KS 筛选器的适配器驱动程序。 系统会通知驱动程序的受保护内容的使用规则。 该驱动程序，反过来，建议 DRMK 任何下游的筛选器，向其路由内容和系统进行身份验证以及这些筛选器。 在关系图完成之前，此过程将继续。 如果数字播放流通过不是符合 DRM 的任何组件，系统将拒绝整个关系图。

DRM 兼容的驱动程序必须防止未经授权的复制在播放数字内容时。 此外，驱动程序必须禁用可以通过标准接口 （例如 S/PDIF) 传输内容通过解密的内容可以捕获的所有数字输出。 请注意，此要求不适用于 USB 设备。 目前，DRMK 只能通过 USB 扬声器设备没有任何数字输出播放安全内容。

 

 




