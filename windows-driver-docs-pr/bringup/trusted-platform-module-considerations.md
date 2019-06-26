---
title: 受信任的平台模块 (TPM) 注意事项
description: 受信任的平台模块 (TPM) 注意事项
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: e131b4782316aecfa65e8ad5f10557c3fcf80dfa
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391754"
---
# <a name="trusted-platform-module-tpm-considerations"></a>受信任的平台模块 (TPM) 注意事项

具有 TPM 2.0 的新设备应为所有 pcr 使用 SHA256。 这不是与下层操作系统兼容。

没有 TPM 2.0 到传统 BIOS 界面。 尽管在这些情况下可以由 Bitlocker 利用 TPM 2.0。  如果当前的硬件上安装 Windows 7，则应安装在 x64 UEFI 启动模式下 （尽管仍将需要 CSM 由于 Windows 7 启动要求），以便您可以从 TPM 2.0 获得的一些好处。

升级到更高版本操作系统后 (Win8 及更高版本)，具体取决于系统上安装固件，您可能能够启用安全启动。 如果在现有硬件上的旧 BIOS 模式下安装 Windows 操作系统，不能接收 TPM 2.0 或安全启动的全部的益处。

## <a name="related-resources"></a>相关资源

[TPM 的建议](https://docs.microsoft.com/windows/security/hardware-protection/tpm/tpm-recommendations)

[受信任的平台模块 2.0:简要介绍](https://trustedcomputinggroup.org/resource/trusted-platform-module-2-0-a-brief-introduction/)

[受信任的平台模块 (TPM)](https://trustedcomputinggroup.org/work-groups/trusted-platform-module/)




