---
title: DRM 要求
description: DRM 要求
ms.assetid: 312b943b-f280-4b29-a5d4-e78c7088bb22
keywords:
- WHQL 测试 WDK 音频
- 数字权限管理 WDK 音频，法规遵从性测试
- DRM WDK 音频，法规遵从性测试
- 法规遵从性测试 WDK 音频
- 测试 DRM 法规遵从性 WDK 音频
- 为 Windows XP 徽标测试 WDK 音频设计
- 徽标测试 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43fd2c78006662f49e1b40abae894afbbf72dade
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360087"
---
# <a name="drm-requirements"></a>DRM 要求


## <span id="drm_requirements"></span><span id="DRM_REQUIREMENTS"></span>


本部分提供音频微型端口驱动程序通过 DRM 法规遵从性测试的 Microsoft Windows 硬件质量实验室 (WHQL) 而必须满足的要求。 这些要求仅适用于 WaveCyclic 和 WavePci[音频微型端口驱动程序](audio-miniport-drivers.md)，这是特定于硬件的对应的端口 Class Library (Portcls.sys) 中的 WavePci 和 WaveCyclic 端口驱动程序。 DRM 法规遵从性测试不是当前适用于 USB 驱动程序。

Windows Me 中和在 Windows XP 及更高版本，仅的受信任音频驱动程序可以播放受 DRM 保护的内容。 Windows 通过特定于 DRM 的数字签名存储在驱动程序的 （目录） 的.cat 文件中标识的受信任的驱动程序。 Microsoft 发布作为由 WHQL 管理硬件兼容性测试的一部分通过 DRM 法规遵从性测试的驱动程序仅的 DRM 签名。

驱动程序 Windows Me，DRM 法规遵从性测试是可选的只在硬件供应商的请求执行。 DRM 签名是单独从，此外还包括 Windows 徽标签名。 请注意，传递 Windows 徽标测试，但不是 DRM 法规遵从性测试的驱动程序仍可以播放不受 DRM 安全的内容。

对于 Windows XP 及更高版本，但是，DRM 法规遵从性测试是 WHQL 测试的必需的部分。 为了获得"设计 Windows XP"徽标的资格，驱动程序必须通过 DRM 法规遵从性测试。

DRM 法规遵从性测试要求受信任的音频驱动程序来执行以下操作：

-   音频的微型端口驱动程序必须实现[IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nn-drmk-idrmaudiostream)接口的 IID 查询时必须返回的对象类型 IDrmAudioStream 其流对象中\_IDrmAudioStream。

-   当请求复制保护 ([**DRMRIGHTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/ns-drmk-tagdrmrights)。**CopyProtect** = **TRUE**)，音频驱动程序必须禁用捕获当前正在播放的流的功能。 这意味着该驱动程序必须将未受保护的数字内容保存到任何形式的非易失性存储，其中包括硬盘，EEPROM、 内存卡以及内存条。 此外，驱动程序必须禁用捕获输出 D/A 转换器上多路复用器，否则阻止的数字内容环回。

-   如果音频驱动程序要求以禁用设备上的数字音频输出 (DRMRIGHTS。**DigitalOutputDisable** = **TRUE**)，它必须禁用能够通过标准接口，通过标准的相互连接方案中传输内容的所有数字音频输出。 数字输出包括-但不是严格限制为-S/PDIF，IEEE 1394 并行、 串行，调制解调器和网络端口。 （此要求不适当前用于 USB。）

-   在处理安全内容时，音频驱动程序必须永远不会附加到其堆栈不受信任的驱动程序。 换而言之，音频驱动程序必须只是依赖还包含 DRM 签名的其他组件。 该驱动程序必须永远不会促进将音频数据传输到不具有 DRM 签名的任何组件。 具体而言，如果驱动程序将数字内容传递给另一个组件，该驱动程序必须使用 DRM Api 在内核中通知[DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver)的这一事实。

除了通过 DRM 法规遵从性测试，音频设备和驱动程序必须允许用户选择的操作模式的失败或 subverts 内核中的 DRM 组件。 具体而言，驱动程序必须提供注册表设置、 用户控件面板或禁用 DRM 函数的其他方式。

 

 




