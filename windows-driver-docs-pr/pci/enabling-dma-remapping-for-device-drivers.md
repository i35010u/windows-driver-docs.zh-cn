---
title: 为设备驱动程序启用 DMA 重新映射
description: 启动并选择直接内存访问 (DMA) 重新映射功能，确保与内核 DMA 保护和 DMAGuard 策略兼容
ms.date: 07/10/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7a5e21322489b2883958da2b33f43efedc5eb9fd
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382001"
---
# <a name="enabling-dma-remapping-for-device-drivers"></a>为设备驱动程序启用 DMA 重新映射

为确保与[内核 DMA 保护](/windows/security/information-protection/kernel-dma-protection-for-thunderbolt)和 [DMAGuard 策略](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)兼容，PCIe 设备驱动程序可选择使用直接内存访问 (DMA) 重新映射。

设备驱动程序的 DMA 重新映射可防止内存损坏和恶意 DMA 攻击，并为设备提供更高级别的兼容性。 此外，具有 DMA 重新映射兼容驱动程序的设备可以启动和执行 DMA，而不考虑锁定屏幕状态。

在启用内核 DMA 保护的系统上，DMAGuard 策略可能会阻止设备，其中包含 DMA 重新映射-不兼容的驱动程序，连接到[外部](./dsd-for-pcie-root-ports.md#identifying-externally-exposed-pcie-root-ports) / [公开](./dsd-for-pcie-root-ports.md#identifying-internal-pcie-ports-accessible-to-users-and-requiring-dma-protection)的 PCIe 端口 (例如，闪电™) ，具体取决于系统管理员设置的策略值。

## <a name="driver-requirements-for-enabling-and-opting-into-dma-remapping"></a>启用和选择 DMA 重映射的驱动程序要求

驱动程序使用以下接口执行 DMA：

* [WDF DMA 接口](../wdf/introduction-to-dma-in-windows-driver-framework.md)
* [WDM 接口](/windows-hardware/drivers/ddi/wdm/)
* [NDIS 接口](/windows-hardware/drivers/ddi/_netvista/)

若要为驱动程序调整 DMA 重新映射策略，请在 "服务安装" 部分添加如下 INF 指令：

  ```inf
    [MyServiceInstall_AddReg]
    HKR,Parameters,DmaRemappingCompatible,0x00010001,1    ; where 1 = opt-in
  ```
  
**DmaRemappingCompatible**的有效值为：

| 值 | 含义 |
| ----- | ------- |
| 0     | 选择退出。这向系统表明你的驱动程序与 DMA 重新映射不兼容。 |
| 1     | 选择启用。 这向系统表明你的驱动程序与 DMA 重新映射完全兼容。 |
| 2     | 选择启用，但仅当满足以下一个或多个条件时：。如果设备是外部设备 (例如。 闪电) ;B.如果在驱动程序验证程序中启用 DMA 验证。 |
| 无注册表项 | 让系统确定策略。 |

测试驱动程序时，请启用驱动程序验证程序。 对于在驱动程序验证程序下进行测试，用于在外部设备中选择的 INF 指令的值将提升为1。

使用启用了 VT-d/AMD-Vi 的 Windows 10 最新内部版本测试 Intel x64 和 AMD64 系统上的驱动程序功能。

> [!NOTE]
> 图形设备驱动程序不支持 DMA 重新映射。

## <a name="validating-that-dma-remapping-is-enabled-for-a-specific-device-driver-instance"></a>验证是否为特定的设备驱动程序实例启用了 DMA 重新映射

若要检查特定驱动程序是否已选择性加入 DMA 重新映射，请在设备的 " **详细信息** " 选项卡中查找与 dma 重新映射策略属性对应的值设备管理器。 驱动程序可以查询这些值的 [**DEVPKEY_Device_DmaRemappingPolicy**](../install/devpkey-device-dmaremappingpolicy.md) 属性。

![“设备管理器详细信息”选项卡](images/device-details-tab-1903.png)

>[!NOTE]
> 对于 Windows 10 版本1803和1809，设备管理器中的属性字段使用 GUID {83da6326-97a6-4088-9453-a1923f573b29} [18]