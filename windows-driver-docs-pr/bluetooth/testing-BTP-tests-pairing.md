---
title: Microsoft 蓝牙测试平台
description: 蓝牙测试平台（BTP）配对测试。
ms.assetid: 19caf4db-9303-47d1-be12-5ff4b2710bc8
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: d85ec8f184c8b834592248867337ec6fb98038f1
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528908"
---
# <a name="btp-pairing-tests"></a>BTP 配对测试 #

BTP 配对测试将测试本地系统如何通过 BR/EDR 或 LE 与远程无线电配对。

## <a name="setting-up-for-testing"></a>设置以供测试 ##

首先检查绿色电源指示器、可选的黄色测试 LED 和 Traduci 上的3个橙色 Led 是否亮起。 确认 SUT 的蓝牙无线电已开机并正确插入到 Traduci 中的适当无线电。 目前，RN42 无线收发器**只能**插入作业。 Simlarly Bluefruit 收音机**只能**插入 JC。 有关设置的更多详细信息，请参阅[设置 BTP](testing-BTP-setup.md)。

支持的无线电设备的信息和购买信息可在[BTP 支持的硬件](testing-BTP-hw.md)上找到。

## <a name="running-the-pairing-tests"></a>运行配对测试 ##

导航到从中提取 BTP 包的文件夹。 它通常位于 `C:\BTP`。 在以包的版本命名的文件夹中，你将找到下面引用的脚本。 然后运行以下任一操作：

- 从提升的命令提示符中 `RunPairingTests.bat <radio name>` 或
- 从提升权限的 PowerShell 控制台 `RunPairingTests.ps1 <radio name>`

有关可用的无线电名称参数的信息，请参阅[设置 BTP](testing-BTP-hw.md#supported-radios)

你还可以在末尾添加可选参数 `-VerboseLogs`，以获取 BTP 的内部操作的更详细的输出。

当测试开始时，12针适配器旁边的红色 LED 将打开，一旦测试中的命令已发送给无线电，就会打开。 每次测试结束时，此 LED 都将关闭。 如果在上一次测试失败时，它在下一次测试开始时处于打开状态，我们将尝试关闭电源，并重新开机，使其返回到已知状态。 如果电源周期失败，则测试将失败，因为无线电处于未知状态。

## <a name="capturing-logs"></a>捕获日志 ##

若要捕获蓝牙日志，请按照[GitHub 上适用于 Windows 存储库的总线工具](https://github.com/microsoft/busiotools/blob/master/bluetooth/tracing/readme.md)中的说明进行操作。

## <a name="known-issues"></a>已知问题 ##

- 压力测试：使用 LE 无线电在严格循环中运行测试可能导致配对或取消配对失败。
