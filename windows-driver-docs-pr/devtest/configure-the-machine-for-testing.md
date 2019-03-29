---
title: 配置用于测试的计算机
description: 概述安装 WDTF 和 TAEF，所需的步骤复制系统基础数据驱动测试，并配置用于测试的计算机
keywords:
- Sysfund 测试
- 数据驱动的测试
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: af161ef2b4f2cc7c70cc0142abd255b62ce9844f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562693"
---
# <a name="configure-the-machine-for-testing"></a>配置用于测试的计算机
本主题概述了安装所需的步骤[WDTF](https://docs.microsoft.com/windows-hardware/drivers/wdtf/)并[TAEF](https://docs.microsoft.com/windows-hardware/drivers/taef/)，复制的数据驱动的测试，并配置用于测试的计算机。 请注意因为 WDTF 安装在系统上安装的驱动程序必须从提升/管理员命令提示符执行以下命令。
下面的说明假定系统体系结构是 x64。  以下步骤可能需要调整为其他体系结构。

**步骤 1**：获取从最新的包和文件[EWDK](https://docs.microsoft.com/windows-hardware/drivers/develop/installing-the-enterprise-wdk)接受许可条款并 EWDK ISO 文件保存到测试将在其中运行的计算机。 EWDK 不需要 Visual Studio 的安装。 只需下载 EWDK ISO、 装载 ISO，并复制以下指定的文件。 若要装载 ISO，右键单击该 ISO 文件，然后单击**装载**。 当它将安装 ISO 驱动器号分配给装载的 ISO。

**步骤 2**:通过导航到已装载的 ISO 中 TAEF MSI 的位置和安装所需的体系结构的包安装 TAEF。 指定的位置和安装日志文件的名称 **%USERPROFILE%\Desktop\TAEFInstall.log**在此示例中：

```console
cd <ISO drive>\Program Files\Windows Kits\10\Testing\Runtimes

msiexec /i "Test Authoring and Execution Framework x64-x64_en-us.msi" /l* "%USERPROFILE%\Desktop\TAEFInstall.log"
```

TAEF MSI 安装到 TAEF `%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\TAEF\x64`。  将此目录添加到系统 PATH 环境变量并重新启动提升的命令提示符。

如果尚未运行，启动 TAEF 服务 (Te.service) 并将设置为**Autostart**通过执行以下步骤。

1.  启动服务： services.msc
2.  Double-click Te.Service
3.  设置为"自动"的"启动"类型
4.  单击开始以启动服务

如果作为服务在 services.msc 中未列出 Te.Service，请转到 **%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\TAEF\x64**并运行以下命令以获取服务已启动：

1. `wex.services.exe /install:te.service` 

   验证已成功安装 te.service

2. `sc start te.service` 

   验证状态是 START_PENDING

3. `sc query te.service` 

   验证状态为正在运行

4. `sc qc te.service` 

   验证的启动类型是 AUTO_START

**步骤 3**:通过导航到 WDTF MSI （上面已装载的 ISO 中 TAEF MSI 与相同的位置） 的位置和安装所需的体系结构的包安装 WDTF。 指定的位置和安装日志文件的名称 **%USERPROFILE%\Desktop\WDTFInstall.log**在此示例中：

```console
cd <ISO drive>\Program Files\Windows Kits\10\Testing\Runtimes
msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64_en-us.msi" /l* "%USERPROFILE%\Desktop\WDTFInstall.log"
```
WDTF MSI 安装到 WDTF **%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\WDTF**。

**步骤 4**:配置用于测试的计算机：

1.  配置计算机以收集完全转储或附加内核调试程序。
2.  因为测试可能可以重新启动计算机并需要控制睡眠周期，永远不会进入睡眠状态，永远不会关闭显示和自动登录到测试帐户 (netplwiz.exe) 将计算机配置。  请注意应谨慎使用该自动登录。

**步骤 5**:通过复制中的所有文件获取数据驱动的测试二进制文件 **\<ISO 驱动器 > files\windows Kits\10\Testing\Tests\Additional Tests\x64\DevFund\DataDriven**到本地文件夹如 **%USERPROFILE%\Desktop\Tests**。 卸载 ISO。

