---
title: 安全启动
description: 安全启动
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 75c73aaf8985e771d421d174d01c05b59606ff2b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189401"
---
# <a name="secure-boot"></a>安全启动

安全启动是一个过程，用于确保你的电脑只使用 PC 制造商信任的软件进行启动。 安全启动不是 Microsoft 独有的，在 UEFI 规范文档中定义，但 Microsoft 确实在下面包括的链接中定义了特定要求。

电脑启动时，固件会检查每个启动软件的签名，包括固件驱动程序 (选项 Rom) 和操作系统。 如果签名良好，则电脑将启动，并且固件会向操作系统提供控制。

Windows 操作系统需要安全启动;Windows 8、8.1 和10也包含在 UEFI 规范文档中。有关其他信息，请参阅 UEFI 规范文档中的 [27.1 安全启动](https://uefi.org/sites/default/files/resources/UEFI_2_3_1_C.pdf) 部分。

有关安全启动的 Windows 要求的详细信息，请参阅下面的**WHCP-1607**链接中的**system.fundamentals.firmware.cs.uefisecureboot.connectedstandby** 。

## <a name="related-resources"></a>相关资源

[硬件安全可测试性规范](/windows-hardware/test/hlk/testref/hardware-security-testability-specification)

[Windows 硬件兼容性计划规范和策略](/windows-hardware/design/compatibility/whcp-specifications-policies)

[1607 WHCP (ZIP 下载) ](https://go.microsoft.com/fwlink/?linkid=866948)

[安全引导和标准引导：强化早期启动组件免受恶意软件侵害](/previous-versions/windows/hardware/design/dn653311(v=vs.85))

[Windows 8.1 安全启动密钥创建和管理指南](/previous-versions/windows/it-pro/windows-8.1-and-8/dn747883(v=win.10))