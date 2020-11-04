---
title: 驱动程序安装测试（设备基础功能）
description: 驱动程序安装测试类别包括多次卸载和重新安装驱动程序以测试安装功能的测试。
ms.assetid: 3FC00D4B-6520-45F1-805C-A5F8B6AACAC8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af1858d53da3138d2dfbe36773127a26afcb656e
ms.sourcegitcommit: ec7bebe3f94536455e62b372c2a28fe69d1717f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93349743"
---
# <a name="driver-install-tests-device-fundamentals"></a>驱动程序安装测试（设备基础功能）

驱动程序安装测试类别包括多次卸载和重新安装驱动程序以测试安装功能的测试。 每次重新安装之后，这些测试将启动针对驱动程序和设备的 i/o 测试。 这些测试旨在提高需要安装和重新安装设备驱动程序或设备的最终用户的总体体验。

## <a name="driverinstall-tests"></a>DriverInstall 测试

### <a name="reinstall-with-io-before-and-after"></a>在之前和之后通过 IO 重新安装

此测试将卸载并重新安装所选设备的驱动程序，并在设备上运行 i/o 测试。

**测试二进制文件** ： Devfund_Reinstall_With_IO_BeforeAndAfter。 wsc

**测试方法** ： Reinstall_With_IO_Before_And_After

**参数** ： [ *DQ* ] 和 [ *IOPeriod* ] 有关详细信息，请参阅 [如何选择和配置设备基础测试](../develop/how-to-select-and-configure-the-device-fundamental-tests.md#device-fundamentals-test-parameters)中的 "设备基础测试参数"。

## <a name="about-the-reinstall-with-io-before-and-after-test"></a>关于测试前后的 i/o 重新安装

此测试执行以下操作：

1. 验证测试设备及其后代是否未报告任何设备问题代码。
2. 使用 WDTF Simple i/o 插件测试测试设备及其后代上的 i/o。 有关详细信息，请参阅 [提供的 WDTF 简单 i/o 插件](../wdtf/provided-wdtf-simpleio-plug-ins.md) 。
3. 使用 [**IWDTFDriverSetupAction2：： UpdateDriver**](/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nf-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2-updatedriver) 方法在测试设备上重新安装原始驱动程序。
4. 验证测试设备及其后代是否未报告任何设备问题代码。
5. 使用 WDTF Simple i/o 插件测试测试设备及其后代上的 i/o。 有关详细信息，请参阅 [提供的 WDTF 简单 i/o 插件](../wdtf/provided-wdtf-simpleio-plug-ins.md) 。
6. 如果步骤 \# 3 需要重新启动，则重新启动系统。
7. 在测试设备上使用 [**IWDTFDriverSetupAction2：： UnInstallDriverPermanently**](/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nf-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2-uninstalldriverpermanently) 方法安装 NULL 驱动程序，以便在需要重新启动时重新启动系统。
8. 使用 [**IWDTFDriverSetupAction2：： UpdateDriver**](/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nf-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2-updatedriver) 方法在受测设备上重新安装原始驱动程序。
9. 验证测试设备及其后代是否未报告任何设备问题代码。
10. 使用 WDTF Simple i/o 插件测试测试设备及其后代上的 i/o。 有关详细信息，请参阅 [提供的 WDTF 简单 i/o 插件](../wdtf/provided-wdtf-simpleio-plug-ins.md) 。
11. 多次重复步骤 1-10。

### <a name="debug-installation-failures-using-the-setup-api-logs"></a>使用安装程序 API 日志调试安装失败

安装 API 日志 (setupapi.log 和 setupapi.log) 包含有用的信息来调试此测试记录的驱动程序安装失败。 在 \\ 测试系统上的% windir% inf 目录下可以找到安装程序 API 日志 \\ 。

若要提高这些日志的详细程度和潜在有用性，请在运行重新安装测试之前，将以下注册表项设置为0x2000FFFF：

```command
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

## <a name="related-topics"></a>相关主题

[如何在运行时使用 Visual Studio 测试驱动程序](/windows-hardware/drivers)

[如何选择和配置设备基础功能测试](/windows-hardware/drivers)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](/windows-hardware/drivers)

[Provided WDTF Simple I/O plug-ins](../wdtf/provided-wdtf-simpleio-plug-ins.md)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](/windows-hardware/drivers)