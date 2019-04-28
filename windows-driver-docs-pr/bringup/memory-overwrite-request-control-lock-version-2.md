---
title: 内存覆盖请求控件 (MOR) LOCK 版本 2
description: 内存覆盖请求控件 (MOR) LOCK 版本 2
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: a86784ffc1142ea38e3dfec682a0120d6bc7a0cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337570"
---
# <a name="memory-overwrite-request-control-mor-lock-version-2"></a>内存覆盖请求控件 (MOR) LOCK 版本 2


Windows 旗舰安全功能 Device Guard 更改内存-机密必须现在从恶意 OS 内核提供保护的虚拟机监控程序中的机密的威胁模型。 这需要扩展 TCG"平台重置攻击的缓解措施"，防止恶意管理员和内核的 RAM 中的机密。 版本 1 定义一个 UEFI 变量的设置时，锁原始 MOR 字节，无法对其正在更改的未经授权代理，例如操作系统内核。 启用设备保护后，原始的多个字节设置为 0x11，指示在平台必须跨所有重置擦除内存 – 禁止自动检测。 这就产生了 Device Guard 已启用的平台上对性能产生负面影响。

锁的版本 2 支持允许经过授权的代理，例如虚拟机监控程序，若要禁用该锁的密钥。 预期结果是，在正常关机，虚拟机监控程序将首先从 RAM 中删除其密钥，使用版本 2 密钥禁用锁，并清除原始的多个字节，启用平台不清除 RAM 的情况下重新启动。 避免性能损失与版本 1 相关联时，固件实现 MOR 锁的版本 2 提供了 Device Guard 机密的保护。 因此，减少意外重新启动攻击的攻击面

在以下版本的 Windows 中包含 MOR 锁 v2 的支持：

-   Windows Server Technical Preview 2016

-   Windows 10 版本 1607 和更高版本


## <a name="related-resources"></a>相关资源

[TCG 平台重置攻击缓解规范](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)

[保护多个实现](https://docs.microsoft.com/windows-hardware/drivers/bringup/device-guard-requirements)



