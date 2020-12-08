---
title: DRM 概述
description: DRM 概述
keywords:
- 数字 Rights Management WDK 音频，关于 DRM
- DRM WDK 音频，关于 DRM
- DRMK 系统驱动程序 WDK 音频
- 解密 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f92d14b2e1c9801cd2cebfec851d90c042bc5452
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789231"
---
# <a name="drm-overview"></a>DRM 概述


## <span id="drm_overview"></span><span id="DRM_OVERVIEW"></span>


适用于数字音频的 DRM 是在 Microsoft Windows 2000 及更高版本和 Windows Me/98 上实现的。 但是，只有 Microsoft Windows XP 和更高版本以及 Windows Me 才能在内核中实施 DRM 安全性。 目前，Windows 不为 MIDI 流或 DLS 集提供 DRM 安全性。

受 DRM 保护的数字内容以加密形式存储在磁盘或其他存储媒体类型上。 加密算法会对内容进行加密，使其在解密之前无法识别。 在播放期间，内容会在从磁盘读取并缓冲到内存中时保持混乱。 在数据路径的末尾附近， [DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver) ( # A0) unscrambles 数据并将其直接送到音频驱动程序，以便播放。 通过限制传输 unscrambled 内容的数据路径的范围，DRMK 使内容不易遭受未经授权的复制。

在 Windows 2000 和 Windows 98 中，通过安全漏洞，用户可以轻松地加载恶意驱动程序，将安全内容的播放以未加密形式传送到磁盘。 Windows XP 和更高版本以及 Windows Me 通过只允许受信任的音频驱动程序来播放受 DRM 保护的内容来关闭此漏洞。

在 Windows XP 及更高版本和 Windows Me 中，安全内容在遍历音频数据路径之前会保持不变，直至进入受保护的内核环境。 在内核中，受保护的组件将数据译码并将 unscrambled 数据馈送到受信任的驱动程序以便播放。 将筛选器图配置为播放 unscrambled 音频流时，DRMK 将为它放置在关系图中的每个 KS 筛选器验证适配器驱动程序。 系统向驱动程序通知受保护内容的使用规则。 相反，驱动程序会建议 DRMK 将内容路由到的任何下游筛选器，系统也会对这些筛选器进行身份验证。 此过程将一直继续，直到图形完成。 如果数字播放流通过任何不符合 DRM 的组件，系统将拒绝整个关系图。

在播放数字内容时，与 DRM 兼容的驱动程序必须阻止未经授权的复制。 此外，驱动程序必须禁用可通过标准接口传输内容的所有数字输出 (例如 S/PDIF) ，可以通过该接口来捕获已解密的内容。 请注意，此要求不适用于 USB 设备。 目前，DRMK 仅通过不带数字输出的 USB 扬声器设备播放安全内容。

 

 




