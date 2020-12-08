---
title: Microsoft 蓝牙测试平台-BTP 电池测试
description: 蓝牙测试平台 (BTP) 电池测试。
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 77d20db9fc91e74e4146e1d9c4d64df647a7d1d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798505"
---
# <a name="btp-battery-tests"></a>BTP 电池测试 #

BTP 电池测试将测试本地系统能否观察配对远程设备上的电池级别变化。

## <a name="setting-up-for-testing"></a>设置以供测试 ##

将收音机与 Traduci 一起使用时，请首先检查绿色电源指示器、可选的黄色测试 LED 和 Traduci 上的3个橙色 Led 是否亮起。 确认 SUT 的蓝牙无线电已打开，并且相应的无线电 () 正确插入到 Traduci。 目前，Bluefruit 收音机 **只能** 插入到 JC 中。 有关设置的更多详细信息，请参阅 [设置 BTP](testing-BTP-setup.md)。

支持的无线收发器的功能和购买信息可在 [支持的 BTP 硬件](testing-BTP-hw.md)上找到。

## <a name="running-the-battery-tests"></a>运行电池测试 ##

导航到从中提取 BTP 包的文件夹。 它通常位于下 `C:\BTP` 。 在以包的版本命名的文件夹中，你将找到下面引用的脚本。 然后运行以下任一文件：

- `RunBatteryTests.bat <radio name>` 从提升的命令提示符或
- `RunBatteryTests.ps1 <radio name>` 从提升权限的 PowerShell 控制台

可在 [此处](testing-BTP-hw.md#supported-radios)找到有关可用的无线电名称参数的信息。

你还可以在末尾添加可选参数 `-VerboseLogs` ，以获取 BTP 的内部操作的更详细输出。

当使用 Traduci 时，如果测试开始，则12针适配器旁边的红色 LED 将会打开，并从测试中的命令开始发出无线电。 每次测试结束时，此 LED 都将关闭。 如果在上一次测试失败时，它在下一次测试开始时处于打开状态，我们将尝试关闭电源，并重新开机，使其返回到已知状态。 如果电源周期失败，则测试将失败，因为无线电处于未知状态。

## <a name="capturing-logs"></a>捕获日志 ##

若要捕获蓝牙日志，请遵循 [GitHub 上的 busiotools For Windows](https://github.com/microsoft/busiotools/blob/master/bluetooth/tracing/readme.md)存储库的说明。
