---
title: 为设备驱动程序启用 DMA 重新映射
description: 启动并选择直接内存访问 (DMA) 重新映射功能，确保与内核 DMA 保护和 DMAGuard 策略兼容
ms.date: 05/16/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3ba29a13a3cc1849512118f2114a5d6f2fca5bc8
ms.sourcegitcommit: 188596c90e03a5619b5cbf0bff4276fc94777253
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84530242"
---
# <a name="enabling-dma-remapping-for-device-drivers"></a>为设备驱动程序启用 DMA 重新映射

为确保与[内核 DMA 保护](https://docs.microsoft.com/windows/security/information-protection/kernel-dma-protection-for-thunderbolt)和 [DMAGuard 策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)兼容，PCIe 设备驱动程序可选择使用直接内存访问 (DMA) 重新映射。

设备驱动程序的 DMA 重新映射可防范内存损坏和恶意 DMA 攻击，并提供更高级别的设备兼容性。 此外，具有与 DMA 重新映射兼容的驱动程序的设备可启动并执行 DMA，而不考虑锁屏界面状态。

在启用了内核 DMA 保护的系统上，DMAGuard 策略可阻止具有与 DMA 重新映射兼容的驱动程序且已连接到[外部](https://docs.microsoft.com/windows-hardware/drivers/pci/dsd-for-pcie-root-ports#identifying-externally-exposed-pcie-root-ports)/[公开](https://docs.microsoft.com/windows-hardware/drivers/pci/dsd-for-pcie-root-ports#identifying-internal-pcie-ports-accessible-to-users-and-requiring-dma-protection) PCIe 端口（如 M.2, Thunderbolt™）的设备，具体取决于系统管理员设置的策略值。

## <a name="driver-requirements-for-enabling-and-opting-into-dma-remapping"></a>关于启用和选择 DMA 重新映射的驱动程序要求

1. 驱动程序使用以下接口执行 DMA：
    * [WDF DMA 接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-dma-in-windows-driver-framework)
    * [WDM 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/)
    * [NDIS 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)
2. 要选择使用 DMA 重新映射，请指定以下 INF 指令：

  ```inf
    [MyServiceInstall_AddReg]
    HKR,Parameters,DmaRemappingCompatible,0x00010001,1
    ;1 = opt-in, 2 = opt-in only for external devices
  ```

3. 在测试驱动程序时启用驱动程序验证程序。
    * 在驱动程序验证程序下（出于测试目的），选择加入外部设备的 INF 指令的值将提升为 1。
4. 使用启用了 VT-d/AMD-Vi 的 Windows 10 最新内部版本测试 Intel x64 和 AMD64 系统上的驱动程序功能。

_注意：图形设备驱动程序不支持 DMA 重新映射。_

## <a name="validating-that-dma-remapping-is-enabled-for-a-specific-device-driver-instance"></a>验证是否已为特定设备驱动程序实例启用 DMA 重新映射

要检查特定驱动程序是否已选择使用 DMA 重新映射，请查看设备管理器中的“详细信息”选项卡，获取与 DMA 重新映射策略属性对应的值。 设备管理器中的策略有 3 个可能的值：

* 2 表示正在为特定设备实例强制实施 DMA 重新映射。
* 1 表示设备驱动程序已明确选择不使用 DMA 重新映射。
* 0（DMA 重新映射策略属性不可见）表示 INF 文件中未指定 DMA 重新映射 INF 指令。 不为此设备强制执行 DMA 重新映射。

>[!NOTE]
> 对于 Windows 10 版本1803和1809，设备管理器中的属性字段使用 GUID {83da6326-97a6-4088-9453-a1923f573b29} [18]
