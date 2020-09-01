---
title: 受信任的平台模块 (TPM) 注意事项
description: 受信任的平台模块 (TPM) 注意事项
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0699c7b0d6233f8bbad25428a63a39d06039bc4f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188683"
---
# <a name="trusted-platform-module-tpm-considerations"></a>受信任的平台模块 (TPM) 注意事项

使用 TPM 2.0 的新设备应将 SHA256 用于所有 PCR 银行。 这可能与下层操作系统不兼容。

TPM 2.0 没有旧式 BIOS 接口。 但在这些方案中，Bitlocker 可以使用 TPM 2.0。  如果在当前硬件上安装 Windows 7，你应该在 x64 UEFI 启动模式下安装 (但是，由于 Windows 7 启动要求，你仍需要一个 CSM) 这样你就可以从 TPM 2.0 获得一些权益。

升级到更高版本的操作系统之后 (Win8 和更高) 版本，根据系统上安装的固件，你可以启用安全启动。 如果在现有硬件上安装旧版 BIOS 模式下的 Windows 操作系统，则无法获得 TPM 2.0 或安全启动的全部权益。

## <a name="related-resources"></a>相关资源

[TPM 建议](/windows/security/hardware-protection/tpm/tpm-recommendations)

[受信任的平台模块2.0：简介](https://trustedcomputinggroup.org/resource/trusted-platform-module-2-0-a-brief-introduction/)

[受信任的平台模块 (TPM)](https://trustedcomputinggroup.org/work-groups/trusted-platform-module/)