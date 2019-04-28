---
title: 数字版权管理
description: 数字版权管理
ms.assetid: 7ce19196-5180-421f-b6be-ac4a235a8c16
keywords:
- WDM 音频驱动程序 WDK，数字权限管理
- 音频驱动程序 WDK，数字权限管理
- 数字权限管理 WDK 音频
- DRM WDK 音频
- 安全 WDK 音频
- 专有数据安全 WDK 音频
- 使用规则 WDK 音频
- 播放规则 WDK 音频
- 加密 WDK 音频
- 加密 WDK 音频
- WDM 音频驱动程序 WDK，安全性
- 音频驱动程序 WDK，安全性
- 受保护内容的 WDK 音频
- 数字内容安全 WDK 音频
- 加密的内容 WDK 音频
- 未经授权的复制 WDK 音频
- 复制保护 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ebb78ebef471b8d786b4dd5561e4f7ea62f1d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333796"
---
# <a name="digital-rights-management"></a>数字版权管理


## <span id="digital_rights_management"></span><span id="DIGITAL_RIGHTS_MANAGEMENT"></span>


数字版权管理 (DRM) 内容提供商提供的手段来保护其专有的音乐或其他数据从未经授权的复制和其他非法用途。 DRM 技术保护数字内容对其进行加密并附加到它确定在其下一个用户可以播放内容的条件的使用规则。 通常，使用规则阻止复制，或限制的内容播放的次数。 操作系统一起使用以强制实施这些规则的驱动程序。

DRM 被旨在作为对用户透明，除非它们尝试违反他们同意这些购买数字内容时使用规则。

只能由受信任的音频驱动程序，可以播放受 DRM 保护的任何数字音频内容。 这些是已通过 microsoft 来验证它们符合 DRM 和包含 DRM 安全措施可以避开通过其没有漏洞的硬件兼容性测试的驱动程序。

此外，调试程序附加到该驱动程序时，不能播放受保护的内容。

Microsoft Windows Me 的驱动程序，WHQL （Microsoft Windows 硬件质量实验室） DRM 符合性测试是可选的。 但是，驱动程序在 Windows XP 及更高版本，请 DRM 法规遵从性是必需的。 有关详细信息，请参阅**DRM 要求**以下列表中的主题。

本部分介绍以下主题：

[DRM 概述](drm-overview.md)

[内容 Id 和内容的权限](content-ids-and-content-rights.md)

[转发 DRM 内容 Id](forwarding-drm-content-ids.md)

[DRM 要求](drm-requirements.md)

[开发和调试 DRM 驱动程序](developing-and-debugging-drm-drivers.md)

[DRM 函数和接口](drm-functions-and-interfaces.md)

 

 




