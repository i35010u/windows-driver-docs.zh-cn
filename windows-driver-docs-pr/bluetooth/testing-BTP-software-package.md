---
title: Microsoft 蓝牙测试平台包
description: 蓝牙测试平台 (BTP) 软件包。
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: f33a8b49622d9c83457be429008d275f058b1d11
ms.sourcegitcommit: b17e8a4c9ed6503e844416b4ca3f8c38199c1b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2021
ms.locfileid: "103193327"
---
# <a name="the-btp-software-package"></a>BTP 软件包

BTP 软件包包含多个用于测试蓝牙方案的工具。

## <a name="download-the-btp-software-package"></a>下载 BTP 软件包

蓝牙测试平台 (BTP) 软件包包含的工具可用于测试支持 Bluetooth 的外设和系统与 Windows 蓝牙堆栈之间的互操作性。 随附的文档简要概述了如何配置硬件并建议拓扑以获得最佳测试范围。 包括有关如何从蓝牙 Windows 堆栈运行测试和收集跟踪事件的过程信息。

[ ![ 下载蓝牙测试平台](images/download.png)](https://download.microsoft.com/download/e/e/e/eeed3cd5-bdbd-47db-9b8e-ca9d2df2cd29/BluetoothTestPlatformPack-1.5.1.msi)软件包下载蓝牙测试平台软件包。

## <a name="version-updates"></a>版本更新

| 版本 | 更改 |
|---------|---------|
|1.5.1     | -添加 BTVS 和 BTETLParse 诊断工具。</br>-对测试可靠性进行了几项修复和改进。 |
|1.4.0     | -添加了对 HID 测试的键盘延迟测试。</br> -向 HID 测试添加了鼠标测试。</br> -添加了音频 + HID 方案测试。 </br> -增加了电池测试。</br> -修复了在较旧的 Windows 版本中运行时导致测试无法加载的问题。</br> -修复了在非本机 CMD/PowerShell 环境上运行时失败的脚本。</br> -对测试可靠性进行了几项修复和改进。 |
|1.3.1     | -添加了支持 A2DP 和 HFP 的音频测试。</br> -通过 Traduci 上的 FPGA 添加了音频音量验证和故障检测。</br> -将测试重命名为更短、更多的用户友好名称。</br> -对测试可靠性进行了几项修复和改进。 |
|1.2.1     | -将 BTP 从专用预览移动到公共预览。</br> -添加了 SleepTests 的新功能，其中演示了执行延迟的命令的 Traduci 功能。</br> -对测试可靠性进行了几项修复和改进。 |

## <a name="tools-in-the-package"></a>包中的工具

### <a name="architecture-independent-files"></a>独立于体系结构的文件

| 测试工具 | 描述 | 文件名 |
| --- | --- | --- |
| ConfigureMachineForBtp | -作为 CMD 脚本和 PowerShell 脚本提供。</br>-配置用于运行 BTP 测试的测试计算机。</br>-计划在新计算机或操作系统安装上运行第一个测试之前运行。</br> | ConfigureMachineForBtp.bat</br>ConfigureMachineForBtp.ps1 |
| RunPairingTests | -作为 CMD 脚本和 PowerShell 脚本提供。</br>-运行蓝牙配对测试。</br>-支持自定义参数（如果提供）。</br> | RunPairingTests.bat</br>RunPairingTests.ps1 |
| RunHIDTests | -作为 CMD 脚本和 PowerShell 脚本提供。</br>-运行蓝牙 HID 测试。</br>-支持自定义参数（如果提供）。</br> | RunHIDTests.bat</br>RunHIDTests.ps1 |
| RunTaefTest | -用于运行 TAEF 测试的 PowerShell 帮助器脚本（给定了测试 dll 名称和测试参数）。</br> | RunTeafTests.ps1 |
| RunAudioTests | -作为 CMD 脚本和 PowerShell 脚本提供。</br>-运行音频测试，包括故障检测和音频音量验证。</br>-支持自定义参数（如果已提供）</br> | RunAudioTests.bat</br>RunAudioTests.ps1 |
| RunAudioHidScenarioTests | -作为 CMD 脚本和 PowerShell 脚本提供。</br>-运行音频和 HID 方案测试。</br>-支持自定义参数（如果已提供）</br> | RunAudioHidScenarioTests.bat</br>RunAudioHidScenarioTests.ps1 |
| RunBatteryTests | -作为 CMD 脚本和 PowerShell 脚本提供。</br>-运行电池测试。</br>-支持自定义参数（如果已提供）</br> | RunBatteryTests.bat</br>RunBatteryTests.ps1 |

### <a name="architecture-dependent-binaries"></a>体系结构相关二进制文件

此表中列出的文件适用于 X86、AMD64 和 ARM64 体系结构。 安装程序将提取每个体系结构的一个实例。

| 测试工具 | 描述 | 文件名 |
| --- | --- | --- |
| BtpDevicePlugin | -支持使用本地 Windows 蓝牙收音机的测试所需的二进制文件。 | Microsoft.Bluetooth.TestPlatform.BtpDevicePlugin.dll |
| GenericSerialIO | -支持使用 Windows 串行通信的 BTP 设备所需的二进制文件。 | Microsoft.Bluetooth.TestPlatform.GenericSerialIO.dll |
| HidTests | -针对蓝牙 HID 测试的测试二进制文件。</br> -可以使用 TAEF 或通过提供的脚本运行。 | TaefHidTests.dll |
| PairingTests | -针对蓝牙配对测试的测试二进制文件。</br> -可以使用 TAEF 或通过提供的脚本运行。 | TaefPairingTests.dll |
| SleepTests | -适用于蓝牙睡眠测试的试验性测试二进制文件。</br> -可以使用 TAEF 运行。 </br>**注意：** 目前不完全支持这种情况。 | TaefSleepTests.dll |
| AudioTests | -针对蓝牙音频测试的测试二进制文件。</br> -可以使用 TAEF 运行。 | TaefAudioTests.dll |
| AudioHidScenarioTests | -针对蓝牙音频和 HID 方案测试的测试二进制文件。</br> -可以使用 TAEF 运行。 | TaefAudioHidScenarioTests.dll |
| BatteryTests | -测试用于蓝牙电池测试的二进制文件。</br> -可以使用 TAEF 运行。 | TaefBatteryTests.dll |
| TraduciCmd | -用于查询和更改 Traduci 状态的命令行工具，包括调试命令。</br> -用于 Traduci 硬件的固件更新。 | TraduciCmd.exe |
| BTETLParse | -用于从支持的 ETL 文件中提取 HCI 跟踪的命令行工具。 | BTETLParse.exe |
| BTVS | -用于流式传输受支持 (格式的实时 HCI 跟踪的图形工具，如 Ellisys、前端和 Wireshark) 。</br> -仅适用于 x86 体系结构。 | btvs.exe |
