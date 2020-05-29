---
title: 内存覆盖请求控件 (MOR) LOCK 版本 2
description: 内存覆盖请求控件 (MOR) LOCK 版本 2
ms.date: 05/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: b3706ffb99d3c8f86f6f19d4b8c42f939c82f14e
ms.sourcegitcommit: 969a98d4866be74e145df617a9f0963053898a0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2020
ms.locfileid: "84153175"
---
# <a name="memory-overwrite-request-control-mor-lock-version-2"></a>内存覆盖请求控制（MOR）锁版本2

为了防止高级内存攻击，将改进现有的系统 BIOS 安全缓解 MemoryOverwriteRequestControl，以支持锁定以应对新的威胁。

版本1定义了一个 UEFI 变量，在设置该变量时，会锁定原始 MOR 字节，以防未经授权的代理（如 OS 内核）对其进行更改。 如果启用了 MOR 锁定，则原始 MOR 字节设置为0x11，表示平台必须擦除所有重置的内存–禁止自动检测。 当启用的平台时，这会导致性能下降。

版本2的锁支持允许授权代理（例如，虚拟机监控程序）禁用锁定的键。 预期是，在正常关闭期间，虚拟机监控程序将首先从 RAM 删除其机密，使用版本2密钥禁用锁定，并清除原始 MOR 字节，使平台能够在不清除 RAM 的情况下重新启动。 实现 MOR 锁版本2的固件提供额外的保护，同时避免与版本1相关的性能损失。

以下 Windows 版本中包含对 MOR Lock V2 的支持：

- Windows Server Technical Preview 2016

- Windows 10 1607 版及更高版本

## <a name="related-resources"></a>相关资源

[TCG 平台重置攻击缓解规范](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)

[安全 MOR 实现](https://docs.microsoft.com/windows-hardware/drivers/bringup/device-guard-requirements)
