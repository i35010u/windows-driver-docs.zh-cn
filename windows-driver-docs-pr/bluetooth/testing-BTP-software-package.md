---
title: Microsoft 蓝牙测试平台
description: 蓝牙测试平台（BTP）软件包。
ms.assetid: a6beeecb-5967-4e08-bfe2-b8aae26861ad
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: c7bac36d57a2e95636a126da771ac49a62c6b5e2
ms.sourcegitcommit: cf3440d9d3ebe3d10d77063092d24be8c94573ba
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82654857"
---
# <a name="the-btp-software-package"></a>BTP 软件包 #

BTP 软件包包含多个用于测试蓝牙方案的工具。

## <a name="download-the-btp-software-package"></a>下载 BTP 软件包 ##

蓝牙测试平台（BTP）软件包包含的工具可用于测试支持 Bluetooth 的外设和系统与 Windows 蓝牙堆栈之间的互操作性。 随附的文档简要概述了如何配置硬件并建议拓扑以获得最佳测试范围。 包括有关如何从蓝牙 Windows 堆栈运行测试和收集跟踪事件的过程信息。

下载蓝牙测试平台软件包[ ![](images/download.png)](//download.microsoft.com/download/e/e/e/eeed3cd5-bdbd-47db-9b8e-ca9d2df2cd29/BluetoothTestPlatformPack-1.3.1.msi) 下载蓝牙测试平台软件包。

## <a name="version-updates"></a>版本更新 ##

| 版本 | 更改 |
| --- | --- |
| 1.3.1 | <ul><li>添加了可运用 A2DP 和 HFP 的音频测试。</li><li>通过 Traduci 上的 FPGA 添加了音频音量验证和故障检测。</li><li>将测试重命名为更短、更多的用户友好名称。</li><li>一些用于测试可靠性的修复和改进。</li><ul> |
| 1.2.1 | <ul><li>将 BTP 从专用预览移动到公共预览。</li><li>添加了实验性 SleepTests，演示执行延迟的命令的 Traduci 的新功能。</li><li>一些用于测试可靠性的修复和改进。</li><ul> |

## <a name="tools-in-the-package"></a>包中的工具 ##

### <a name="architecture-independent-files"></a>独立于体系结构的文件 ###

| 测试工具 | 说明 | Filename |
| --- | --- | --- |
| ConfigureMachineForBtp | <ul><li>作为 CMD 脚本和 PowerShell 脚本提供。</li><li>配置用于运行 BTP 测试的测试计算机。</li><li>计划在新的计算机上运行首次测试或安装的操作系统。</li> | ConfigureMachineForBtp<br>ConfigureMachineForBtp |
| RunPairingTests | <ul><li>作为 CMD 脚本和 PowerShell 脚本提供。</li><li>运行蓝牙配对测试。</li><li>支持自定义参数（如果提供）。</li></ul> | RunPairingTests<br>RunPairingTests |
| RunHIDTests | <ul><li>作为 CMD 脚本和 PowerShell 脚本提供。</li><li>运行蓝牙 HID 测试。</li><li>支持自定义参数（如果提供）。</li></ul> | RunHIDTests<br>RunHIDTests |
| RunTaefTest | <ul><li>给定测试 dll 名称和测试参数，用于运行 TAEF 测试的 PowerShell 帮助器脚本。</li></ul> | RunTeafTests |
| RunAudioTests | <ul><li>作为 CMD 脚本和 PowerShell 脚本提供。</li><li>运行音频测试，包括故障检测和音频音量验证。</li><li>支持自定义参数（如果已提供）</li></ul> | RunAudioTests<br>RunAudioTests |

### <a name="architecture-dependent-binaries"></a>体系结构相关二进制文件 ###

此表中列出的文件适用于 X86、AMD64 和 ARM64 体系结构。 安装程序将提取每个体系结构的一个实例。

| 测试工具 | 说明 | Filename |
| --- | --- | --- |
| HidTests | <ul><li>针对蓝牙 HID 测试的测试二进制文件。</li><li>可以使用 TAEF 或通过提供的脚本运行。</li></ul> | TaefHidTests |
| HidInputObserver | <ul><li>支持 HID 测试所需的二进制文件。</li></ul> | TestPlatform. HidInputObserver .dll |
| LocalRadioAdapter | <ul><li>支持使用本地 Windows 蓝牙收音机的测试所需的二进制文件。</li></ul> | TestPlatform. LocalRadioAdapter .dll |
| TraduciInputOutput | <ul><li>支持使用 Traduci 的测试所需的二进制文件。</li></ul> | TestPlatform. TraduciInputOutput .dll |
| PairingTests | <ul><li>测试适用于蓝牙配对测试的二进制文件。</li><li>可以使用 TAEF 或通过提供的脚本运行。</li></ul> | TaefPairingTests |
| SleepTests | <ul><li>适用于蓝牙睡眠测试的实验性测试二进制文件。</li><li>可以使用 TAEF 运行。</li><li> <b>注意：</b>目前不完全支持这种情况。</li></ul> | TaefSleepTests |
| AudioTests | <ul><li>测试适用于蓝牙音频测试的二进制文件。</li><li>可以使用 TAEF 运行。</li></ul> | TaefAudioTests |
| TraduciCmd | <ul><li>用于查询和更改 Traduci 状态的命令行工具，包括调试命令。</li><li>用于 Traduci 硬件的固件更新。</li></ul> | TraduciCmd |
