---
title: DRM 要求
description: DRM 要求
ms.assetid: 312b943b-f280-4b29-a5d4-e78c7088bb22
keywords:
- WHQL 测试 WDK 音频
- 数字 Rights Management WDK 音频，合规性测试
- DRM WDK 音频，合规性测试
- 合规性测试 WDK 音频
- 测试 DRM 相容性 WDK 音频
- 为 Windows XP 徽标测试 WDK 音频设计
- 徽标测试 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 106987b978584501bafa20e93642f63d35856028
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208051"
---
# <a name="drm-requirements"></a>DRM 要求


## <span id="drm_requirements"></span><span id="DRM_REQUIREMENTS"></span>


本部分介绍音频微型端口驱动程序必须满足的要求，以通过 Microsoft Windows 硬件质量实验室 (WHQL) 传递 DRM 遵从性测试。 这些要求专门适用于 WaveCyclic 和 WavePci [音频微型端口驱动程序，这些驱动程序](audio-miniport-drivers.md)是与端口类库中的 WavePci 和 WaveCyclic 端口驱动程序的特定于硬件的对应项 ( # A0) 。 DRM 遵从性测试当前不适用于 USB 驱动程序。

在 Windows Me 和 Windows XP 及更高版本中，只有受信任的音频驱动程序可以播放受 DRM 保护的内容。 Windows 通过特定于 DRM 的数字签名来标识受信任的驱动程序，该数字签名存储在驱动程序的 .cat (目录) 文件中。 Microsoft 仅为作为 WHQL 管理的硬件兼容性测试的一部分的驱动程序颁发了 DRM 签名。

对于 Windows Me 驱动程序，DRM 相容性测试是可选的，仅在硬件供应商的请求中执行。 除 Windows 徽标签名外，DRM 签名还独立于和。 请注意，通过 Windows 徽标测试但不是 DRM 相容性测试的驱动程序仍可播放不受 DRM 安全保护的内容。

但对于 Windows XP 和更高版本，DRM 遵从性测试是 WHQL 测试的必需部分。 驱动程序必须通过 DRM 遵从性测试，才能符合 "专为 Windows XP" 徽标。

DRM 相容性测试要求使用受信任的音频驱动程序来执行以下操作：

-   音频微型端口驱动程序必须在其流对象中实现 [IDrmAudioStream](/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream) 接口，如果查询了 IID IDrmAudioStream，则必须返回 IDrmAudioStream 类型的对象 \_ 。

-    ([**DRMRIGHTS**](/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmrights)请求复制保护时。**CopyProtect**  = **如果**) ，则音频驱动程序必须禁用捕获当前播放的流的功能。 这意味着，驱动程序不能将未受保护的数字内容保存到任何形式的非易失性存储，包括硬盘、EEPROM、内存卡和内存条。 同时，驱动程序必须禁用输出 D/A 转换器上的捕获多路复用器，否则会阻止数字内容的环回。

-   当要求音频驱动程序在设备上禁用数字音频输出时 (DRMRIGHTS。**DigitalOutputDisable**  = **) ，** 它必须禁用所有能够通过标准互连方案通过标准接口传输内容的数字音频输出。 数字输出包括--但并不严格限制为--S/PDIF、IEEE 1394、并行、串行、调制解调器和网络端口。  (此要求目前不适用于 USB。 ) 

-   处理安全内容时，音频驱动程序绝不能将不受信任的驱动程序附加到其堆栈。 换句话说，音频驱动程序必须仅依赖于另外包含 DRM 签名的其他组件。 驱动程序决不能促进音频数据到没有 DRM 签名的任何组件的传输。 特别是，如果驱动程序将数字内容传递到另一个组件，则驱动程序必须使用内核中的 DRM Api 来通知 [DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver) 的情况。

除了传递 DRM 相容性测试以外，音频设备和驱动程序不得允许用户选择在内核中破坏或 subverts DRM 组件的操作模式。 具体而言，驱动程序不得提供注册表设置、用户控制面板或禁用 DRM 功能的其他方法。

 

