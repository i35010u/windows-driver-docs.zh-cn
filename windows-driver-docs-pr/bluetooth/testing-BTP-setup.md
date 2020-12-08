---
title: Microsoft 蓝牙测试平台安装程序
description: 如何设置 Microsoft 蓝牙测试平台安装程序
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 512c124ed32cfa8f15b22d6155a9d024a178c9a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798515"
---
# <a name="setting-up-the-bluetooth-test-platform-btp"></a>设置蓝牙测试平台 (BTP) 

## <a name="hardware-setup"></a>硬件设置

### <a name="connecting-traduci-to-the-pc"></a>将 Traduci 连接到电脑

使用提供的 USB A 到 B 电缆，将 Traduci 插入测试 (SUT) 的系统上的 USB 端口。 如果将 Traduci 直接插入 PC 上的某个端口，并且 Traduci 由 [9v，2a power adapter](https://www.digikey.com/product-detail/en/qualtek/QFWB-18-9-US01/Q1181-ND/8260129) 通过 USB 连接器右侧的圆筒形连接器供电，则性能最佳。 请勿将 Traduci 连接到 USB 集线器。

![显示 USB 和电源端口的 Traduci 电路板的倾斜侧视图。](images/Traduci_USBPortSidejpg.jpg)

### <a name="connecting-peripherals-to-the-traduci"></a>将外围设备连接到 Traduci

Traduci 具有 4 12 针端口 (标签为 JA、作业、JC、JD) 用于测试外围设备。

![显示 USB 和电源端口的 Traduci](images/Traduci_12PinPortSide.jpg)

若要将外围广播插入到 Traduci 上的端口，请定向 Traduci，使 Led 和按钮正面朝上。 接下来定向收音机滑板，使无线电设备上包含 MAC 地址和任何开关的打印标签正面朝上。 保持此方向，将外围广播插入到适当的12个 pin 端口。

> [!NOTE]
> 某些外设只能插入特定端口。  有关详细信息，请参阅 [支持的硬件页](testing-BTP-hw.md) 。

![已插入外设的 Traduci](images/Traduci_and_DigilentRN42.jpg)

## <a name="software-setup"></a>软件设置

1. 下载 [Windows 驱动程序工具包](../download-the-wdk.md#download-icon-step-2-install-wdk-for-windows-10-version-2004)。

2. 安装 WDK 之后 [ (TAEF) ](../taef/index.md) 安装文件 ( * .msi 和 * .cab 文件) 位于目录中的安装文件 `%ProgramFiles%\Windows Kits\10\Testing\Runtimes` 。

3. 下载 BTP 软件包，该 [软件包](testing-BTP-software-package.md)会将所有所需的文件安装到 `C:\BTP` 目录。

4. 确保 **禁用**[安全启动](/windows-hardware/design/device-experiences/oem-secure-boot)。

5. 确保 **禁用** BitLocker。

6. 确保将 Traduci 板插入 SUT。

7. 在 SUT 上提升的命令行中，导航到该 `C:\BTP` 目录，然后运行 `ConfigureMachineForBTP.bat` 以配置测试计算机。 可能需要重新启动。

8. 请参阅 [BTP 测试](testing-BTP-Tests.md) ，以在包中运行测试脚本。

## <a name="known-issues"></a>已知问题

- 电源：如果设备插入到未接通电源的集线器或 VCC 无法提供5V，可能会出现间歇性故障。 在这些情况下，请使用已通电的 USB 集线器或使用9V 的 AC-DC 圆筒适配器。
