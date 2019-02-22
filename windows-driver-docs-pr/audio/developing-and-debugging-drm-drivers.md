---
title: 开发和调试 DRM 驱动程序
description: 开发和调试 DRM 驱动程序
ms.assetid: 3450717a-fd27-4bea-8740-9d47b420ed32
keywords:
- 数字权限管理 WDK 音频，建议
- DRM WDK 音频，建议
- 数字权限管理 WDK 音频，调试
- DRM WDK 音频，调试
- 调试驱动程序 WDK DRM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d05032f85e6b2de8e81f145a41a92dd6c37d304
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546558"
---
# <a name="developing-and-debugging-drm-drivers"></a>开发和调试 DRM 驱动程序


## <span id="developing_and_debugging_drm_drivers"></span><span id="DEVELOPING_AND_DEBUGGING_DRM_DRIVERS"></span>


以下清单可帮助避免一些常见缺陷的驱动程序编写人员：

-   如果该驱动程序禁用批扩展捕获和 S/PDIF 输出而受 DRM 保护内容播放，驱动程序应记得再次将其启用后播放受 DRM 保护的内容完成 （和销毁 DRM 缓冲区）。

-   如果设备执行混合使用的硬件，该驱动程序应跟踪的复合的使用权限时发生流添加到或删除的混合环境中的任何更改。 随时组合包括一个或多个受版权保护 DRM 流，例如，捕获应处于静音状态。 如果播放受保护的组合时捕获已开启，它应保留静音。

-   后向筛选器关系图或与流相关联的属性设置的更改，该驱动程序可能需要立即更新的流复制保护并允许设置输出。 该驱动程序应同步其操作，以防止受保护的内容复制到捕获缓冲区或数字输出。 例如，当捕获多路复用器更改到的输入的流，该驱动程序不应允许安全内容以提供静音打开和关闭所需的时间内变得易受攻击。

[DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver)会阻止内核调试程序连接时播放受 DRM 保护的内容。 反调试破解是 DRMK 使用发出受保护的内容不透明的多个度量值之一。 但是，一旦您的驱动程序已准备好进行测试，您可以通过使用以下技术调试其符合 DRM 的功能：

-   临时修改批流**SetState**方法 (有关示例，请参阅[ **IMiniportWavePciStream::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536733)) 来调用[ **IDrmAudioStream::SetContentId** ](https://msdn.microsoft.com/library/windows/hardware/ff536570)并设置[ **DRMRIGHTS** ](https://msdn.microsoft.com/library/windows/hardware/ff536355)参数的**CopyProtect**成员添加到 **，则返回 TRUE**。

-   完成调试后，请务必删除**SetContentId**调用。

通过此方法，您可以播放未受保护的内容，就好像它是受 DRM 保护的内容，但尽量不要禁用调试器。

例如，可以使用调试器验证，您的驱动程序可防止内容被记录。 尝试诱使驱动程序通过更改 SndVol32 程序的卷启用通过捕获 MUX 批扩展流的录制，并且将设置设为静音。 滑块应反映您对其设置是持久的但 MUX 应继续将批扩展流调节到静音"受保护"的内容完成播放之前捕获的更改。 新设置才会生效。

 

 




