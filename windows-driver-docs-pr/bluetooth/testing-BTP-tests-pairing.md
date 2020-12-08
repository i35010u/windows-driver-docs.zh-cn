---
title: Microsoft 蓝牙测试平台配对
description: " (BTP) 配对测试的蓝牙测试平台。"
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7910f1c9b22aa15ef4f8a180952d45bd528086dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798495"
---
# <a name="btp-pairing-tests"></a>BTP 配对测试

BTP 配对测试将测试本地系统如何通过 BR/EDR 或 LE 与远程无线电配对。

## <a name="setting-up-for-testing"></a>设置以供测试

将收音机与 Traduci 一起使用时，请首先检查绿色电源指示器、可选的黄色测试 LED 和 Traduci 上的3个橙色 Led 是否亮起。 确认 SUT 的蓝牙无线电已打开，并且相应的无线电 () 正确插入到 Traduci。 目前，RN42 无线收发器 **只能** 插入作业。 Simlarly Bluefruit 收音机 **只能** 插入 JC。 有关设置的更多详细信息，请参阅 [设置 BTP](testing-BTP-setup.md)。

当使用 BM.EXE-64-EVB 时，应 (两个红色 Led，其中一条可能在) 一次后关闭。 确认在 [bm.exe-64-EVB 板概述](testing-BTP-hw-bm64.md#getting-started)中，将开关、跳线和端口配置为以述的形式进行测试。

支持的无线收发器的功能和购买信息可在 [支持的 BTP 硬件](testing-BTP-hw.md)上找到。

## <a name="running-the-pairing-tests"></a>运行配对测试

导航到从中提取 BTP 包的文件夹。 它通常位于下 `C:\BTP` 。 在以包的版本命名的文件夹中，你将找到下面引用的脚本。 然后运行以下任一文件：

- `RunPairingTests.bat <radio name>` 从提升的命令提示符或
- `RunPairingTests.ps1 <radio name>` 从提升权限的 PowerShell 控制台

可在 [此处](testing-BTP-hw.md#supported-radios)找到有关可用的无线电名称参数的信息。

你还可以在末尾添加可选参数 `-VerboseLogs` ，以获取 BTP 的内部操作的更详细输出。

当使用 Traduci 时，如果测试开始，则12针适配器旁边的红色 LED 将会打开，并从测试中的命令开始发出无线电。 每次测试结束时，此 LED 都将关闭。 如果在上一次测试失败时，它在下一次测试开始时处于打开状态，我们将尝试关闭电源，并重新开机，使其返回到已知状态。 如果电源周期失败，则测试将失败，因为无线电处于未知状态。

当使用 BM.EXE-64-EVB 时，红和蓝 Led 将以模式进行闪烁，以获取进程的该值指示步骤，如开机和配对。

## <a name="capturing-logs"></a>捕获日志

若要捕获蓝牙日志，请遵循 [GitHub 上的 busiotools For Windows](https://github.com/microsoft/busiotools/blob/master/bluetooth/tracing/readme.md)存储库的说明。

## <a name="known-issues"></a>已知问题

- 压力测试：使用 LE 无线电在严格循环中运行测试可能导致配对或取消配对失败。
