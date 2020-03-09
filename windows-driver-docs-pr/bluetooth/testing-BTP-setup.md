---
title: Microsoft 蓝牙测试平台安装程序
description: BTP 安装程序
ms.date: 2/14/2020
ms.assetid: 85ac7c5b-b5f7-49e0-85f8-72e191c00974
ms.localizationpriority: medium
ms.openlocfilehash: 4d1ed88ea816d5b08bb74afc48871881826949e2
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528914"
---
# <a name="setting-up-the-bluetooth-test-platform-btp"></a>设置蓝牙测试平台（BTP） #

## <a name="hardware-setup"></a>硬件安装 ##

### <a name="connecting-traduci-to-the-pc"></a>将 Traduci 连接到电脑 ###

使用提供的 USB A 到 B 电缆，将 Traduci 插入到正在测试的系统（SUT）上的 USB 端口中。 如果将 Traduci 直接插入 PC 上的某个端口，并且 Traduci 由[9v，2a power adapter](https://www.digikey.com/product-detail/en/qualtek/QFWB-18-9-US01/Q1181-ND/8260129)通过 USB 连接器右侧的圆筒形连接器供电，则性能最佳。 请勿将 Traduci 连接到 USB 集线器。

![显示 USB 和电源端口的 Traduci](images/Traduci_USBPortSidejpg.jpg)

### <a name="connecting-peripherals-to-the-traduci"></a>将外围设备连接到 Traduci ###

Traduci 具有 4 12 针端口（标记为 JA、作业、JC、JD）用于测试外围设备。

![显示 USB 和电源端口的 Traduci](images/Traduci_12PinPortSide.jpg)

若要将外围广播插入到 Traduci 上的端口，请定向 Traduci，使 Led 和按钮正面朝上。 接下来定向收音机滑板，使无线电设备上包含 MAC 地址和任何开关的打印标签正面朝上。 保持此方向，将外围广播插入到适当的12个 pin 端口。

> [!NOTE]
> 某些外设只能插入特定端口。  有关详细信息，请参阅[支持的硬件页](testing-BTP-hw.md)。

![已插入外设的 Traduci](images/Traduci_and_DigilentRN42.jpg)

## <a name="software-setup"></a>软件设置 ##

1. 下载[Windows 驱动程序工具包](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk#download-icon-step-2-install-wdk-for-windows-10-version-1903)。

2. 安装 WDK 后，[测试创作和执行框架（TAEF）](https://docs.microsoft.com/windows-hardware/drivers/taef/)安装文件（* .msi 和 * .cab 文件）位于 `%ProgramFiles%\Windows Kits\8.0\Testing\Runtimes` 目录中。

3. 下载 BTP 软件包，该[软件包](testing-BTP-software-package.md)会将所有必需的文件安装到 `C:\BTP` 目录。

4. 确保**禁用**[安全启动](https://docs.microsoft.com/windows-hardware/design/device-experiences/oem-secure-boot)。

5. 确保**禁用**BitLocker。

6. 确保将 Traduci 板插入 SUT。

7. 在 SUT 上提升的命令行中，导航到 `C:\BTP` 目录，并运行 `ConfigureMachineForBTP.bat` 来配置测试计算机。 可能需要重新启动。

8. 请参阅[BTP 测试](testing-BTP-Tests.md)，以在包中运行测试脚本。

## <a name="known-issues"></a>已知问题 ##

- 电源：如果设备插入到未接通电源的集线器或 VCC 无法提供5V，可能会出现间歇性故障。 在这些情况下，请使用已通电的 USB 集线器或使用9V 的 AC-DC 圆筒适配器。