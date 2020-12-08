---
title: 数字版权管理
description: 数字版权管理
keywords:
- WDM 音频驱动程序 WDK、数字 Rights Management
- 音频驱动程序 WDK，数字 Rights Management
- 数字 Rights Management WDK 音频
- DRM WDK 音频
- 安全 WDK 音频
- 专有数据安全性 WDK 音频
- 使用规则 WDK 音频
- 播放规则 WDK 音频
- 加密 WDK 音频
- 加密 WDK 音频
- WDM 音频驱动程序 WDK，安全性
- 音频驱动程序 WDK，安全性
- 受保护的内容 WDK 音频
- 数字内容安全性 WDK 音频
- 编码的内容 WDK 音频
- 未经授权复制 WDK 音频
- 复制保护 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caece4a28198d90ef0c737b569a74b584610dc70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789291"
---
# <a name="digital-rights-management"></a>数字版权管理


## <span id="digital_rights_management"></span><span id="DIGITAL_RIGHTS_MANAGEMENT"></span>


数字 Rights Management (DRM) 为内容提供商提供保护其专有音乐或其他数据免遭未经授权的复制和其他非法用途的手段。 DRM 技术通过加密来保护数字内容并附加到 it 使用规则，确定用户可以播放内容的条件。 使用规则通常会阻止复制或限制内容的播放次数。 操作系统与驱动程序配合使用来实施这些规则。

DRM 被设计为对用户透明，除非他们尝试违反他们在购买数字内容时同意的使用规则。

受 DRM 保护的任何数字音频内容只能由受信任的音频驱动程序播放。 这些驱动程序已通过 Microsoft 的硬件兼容性测试来验证它们是否符合 DRM 规范，并且不包含任何漏洞，可以通过该驱动程序规避 DRM 安全措施。

此外，当调试器附加到驱动程序时，不能播放受保护的内容。

对于 Microsoft Windows Me 驱动程序，WHQL (Microsoft Windows 硬件质量实验室) 对 DRM 相容性的测试是可选的。 但是，对于 Windows XP 和更高版本中的驱动程序，需要 DRM 相容性。 有关详细信息，请参阅以下列表中的 **DRM 要求** 主题。

本部分介绍以下主题：

[DRM 概述](drm-overview.md)

[内容 ID 和内容权限](content-ids-and-content-rights.md)

[转发 DRM 内容 ID](forwarding-drm-content-ids.md)

[DRM 要求](drm-requirements.md)

[开发和调试 DRM 驱动程序](developing-and-debugging-drm-drivers.md)

[DRM 函数和接口](drm-functions-and-interfaces.md)

 

 




