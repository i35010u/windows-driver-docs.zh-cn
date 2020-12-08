---
title: 开发和调试 DRM 驱动程序
description: 开发和调试 DRM 驱动程序
keywords:
- 数字 Rights Management WDK 音频，建议
- DRM WDK 音频，建议
- 数字 Rights Management WDK 音频，调试
- DRM WDK 音频，调试
- 调试驱动程序 WDK DRM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74e508071368ada96544971226d6273ab5c6e8ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789295"
---
# <a name="developing-and-debugging-drm-drivers"></a>开发和调试 DRM 驱动程序


## <span id="developing_and_debugging_drm_drivers"></span><span id="DEVELOPING_AND_DEBUGGING_DRM_DRIVERS"></span>


下列清单可帮助驱动程序编写器避免一些常见的缺陷：

-   如果驱动程序在播放受 DRM 保护的内容时禁用了波形捕获和 S/PDIF 输出，则驱动程序应记得在受 DRM 保护的内容完成播放之后再次启用它们 (并且 DRM 缓冲区已) 销毁。

-   如果设备执行硬件混合，驱动程序应跟踪在组合中添加或删除流时所发生的复合使用权限变化。 任何组合都包含一个或多个受保护的受保护 DRM 流，例如，应将捕获设为静音。 如果在受保护的组合正在播放时打开捕获，则它应保持为静音。

-   更改筛选器关系图或与流关联的属性设置之后，驱动程序可能需要立即更新流的复制保护和输出启用设置。 驱动程序应同步其操作，以阻止受保护的内容复制到捕获缓冲区或数字输出。 例如，当捕获的输入流发生变化时，驱动程序不会允许安全内容在打开和关闭静音所需的时间内变得易受攻击。

[DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver)可防止在播放受 DRM 保护的内容时内核调试器连接。 反调试防御是 DRMK 用于使受保护内容透明的几个措施之一。 但是，一旦你的驱动程序准备好进行测试，你就可以使用以下技术调试其 DRM 兼容的功能：

-   临时修改波形流的 **SetState** 方法 (例如，请参阅 [**IMiniportWavePciStream：： SetState**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setstate)) 调用 [**IDrmAudioStream：： SetContentId**](/windows-hardware/drivers/ddi/drmk/nf-drmk-idrmaudiostream-setcontentid) ，并将 [**DRMRIGHTS**](/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmrights) 参数的 **CopyProtect** 成员设置为 **TRUE**。

-   完成调试后，请记得删除 **SetContentId** 调用。

利用此方法，你可以播放未受保护的内容，就像它是受 DRM 保护的内容一样，但要避免禁用调试器。

例如，可以使用调试器来验证驱动程序是否阻止记录内容。 尝试通过更改 SndVol32 程序的 "卷" 和 "静音" 设置，欺骗驱动程序启用通过捕获 MUX 记录波形流。 滑块应反映您对其设置所做的更改，这些更改是持久性的，但捕获 MUX 应继续对波形流进行静音，直到 "受保护的内容" 完成播放。 只有这样才能使新设置生效。

 

