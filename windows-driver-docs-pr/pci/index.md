---
title: PCI 驱动程序编程指南
description: PCI 驱动程序编程指南
ms.assetid: 014f6243-6166-42e1-9f0f-1a438c77fd78
keywords:
- PCI WDK 总线
- 总线 WDK，PCI
- 外设组件互连 WDK 总线
- PCI 本地总线规范 WDK
- 配置空间 WDK PCI
- 特定于设备的配置空间 WDK PCI
- 请求配置空间信息 WDK PCI
- 电源管理 WDK PCI
- 查询电源管理功能数据
- 标题 WDK PCI
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 6d47f516f8a698b875ef273d1571a5174e95f365
ms.sourcegitcommit: 9b3dec2f2cd9a7ed9b340b4794ce6ff4134d8ebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91787645"
---
# <a name="pci-driver-programming-guide"></a>PCI 驱动程序编程指南

下表汇总了不同版本的 Windows 支持的 PCIe 功能。 有关详细信息，请参阅[官方 PCIe 规范](https://pcisig.com/specifications/review-zone)中的指定部分。

|功能|最大 Windows 版本|
|----|----|
|大小可调整的栏功能</br>请参阅 7.22 部分。|Windows 10|
|原子操作</br>请参阅 6.15 部分。|Windows 10|
|用于优化 FW 延迟的 ACPI 添加件</br>请参阅[用于优化 FW 延迟的 ACPI 添加件](https://pcisig.com/specifications)|Windows 10|
|ATS/PRI</br>-  [ATS 规范](https://go.microsoft.com/fwlink/p/?LinkId=787061)</br>-  [PCI Express&#174; 基础规范修订版 3.1、单根 I/O 虚拟化和共享修订版 1.1、地址转换和共享修订版 1.1 和 M.2 规范修订版 1.0 的勘误表](https://pcisig.com/specifications/iov/)|Windows 10|
|优化的缓冲区刷新/填充 (OBFF)</br>请参阅 6.19 部分。|- Windows 8</br>- Windows Server 2012|
|延迟容限报告 (LTR) 功能</br>请参阅 7.25 部分。|- Windows 8</br>- Windows Server 2012|
|替代路由 ID 解释 (ARI)</br>请参阅 6.13 部分。|- Windows 8</br>- Windows Server 2012|
|消息信号中断 (MSI/MSI-X) 支持</br>请参阅 6.1.4 部分。|- Windows Vista</br>- Windows Server 2008 R2|
|TLP 处理提示 (TPH)</br>请参阅 6.17 部分。|- Windows 8</br>- Windows Server 2012|
|单根 I/O 虚拟化 (SR-IOV)</br>请参阅[单根 I/O 虚拟化 (SR-IOV)](../network/single-root-i-o-virtualization--sr-iov-.md)。|- Windows 8</br>- Windows Server 2012|

## <a name="in-this-section"></a>本节内容

- [PCI 电源管理和设备驱动程序](./pci-power-management-and-device-drivers.md)
- [访问 PCI 设备配置空间](./accessing-pci-device-configuration-space.md)
- [减少 I/O 资源使用](./i-o-resource-usage-reduction.md)
- [启动设备 IRP 中的资源顺序](./order-of-resources-in-start-device-irp.md)
- [有关图形的 PCI Express 常见问题解答](./pci-express-faq-for-graphics.md)
- [PCI 示例](./pci-sample.md)

## <a name="see-also"></a>另请参阅

[官方 PCIe 规范](https://pcisig.com/specifications/review-zone)
