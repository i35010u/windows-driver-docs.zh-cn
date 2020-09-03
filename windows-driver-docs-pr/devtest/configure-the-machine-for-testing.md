---
title: 配置用于测试的计算机
description: 安装 WDTF 和 TAEF 所需步骤的大纲，复制系统基础数据驱动的测试，并将计算机配置为进行测试
keywords:
- Sysfund 测试
- 数据驱动的测试
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: df2d43c3e460c7cd74342ab1b4461a6147d076ec
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383997"
---
# <a name="configure-the-machine-for-testing"></a>配置用于测试的计算机
本主题概述了安装 [WDTF](../wdtf/index.md) 和 [TAEF](../taef/index.md)所需的步骤，如何复制数据驱动的测试，以及如何配置计算机以进行测试。 请注意，必须在提升的/管理员命令提示符下执行以下命令，因为 WDTF 安装会在系统上安装驱动程序。
以下说明假定系统体系结构为 x64。  对于其他体系结构，可能需要调整以下步骤。

**步骤 1**：通过接受许可条款并将 EWDK ISO 文件保存到运行测试的计算机上，从最新 [EWDK](../develop/using-the-enterprise-wdk.md) 获取包和文件。 EWDK 无需安装 Visual Studio。 只需下载 EWDK ISO，装载 ISO，并复制下面指定的文件。 若要装载 ISO，请右键单击该 ISO 文件，然后单击 " **装载**"。 装载后，会将 ISO 驱动器号分配给已装载的 ISO。

**步骤 2**：通过导航到已装载的 ISO 中 TAEF MSI 的位置并为所需的体系结构安装包来安装 TAEF。 指定安装日志文件的位置和名称，在此示例中为 **%USERPROFILE%\Desktop\TAEFInstall.log** ：

```console
cd <ISO drive>\Program Files\Windows Kits\10\Testing\Runtimes

msiexec /i "Test Authoring and Execution Framework x64-x64_en-us.msi" /l* "%USERPROFILE%\Desktop\TAEFInstall.log"
```

TAEF MSI 将 TAEF 安装到 `%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\TAEF\x64` 。  将此目录添加到系统路径环境变量，然后重新启动提升的命令提示符。

如果该服务尚未运行，请按照以下步骤操作，启动 TAEF service (Te) 并将其设置为 **自动启动** 。

1.  启动服务： services.msc
2.  双击 "Te"。服务
3.  将 "启动" 类型设置为 "自动"
4.  单击 "启动" 以启动服务

如果服务未在 services.msc 中列出为服务，请转到 **%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\TAEF\x64** ，并运行以下命令以启动该服务：

1. `wex.services.exe /install:te.service` 

   验证 te. 服务是否已成功安装

2. `sc start te.service` 

   验证 "状态" 是否为 "START_PENDING"

3. `sc query te.service` 

   验证 "状态" 是否为 "正在运行"

4. `sc qc te.service` 

   验证 "START_TYPE" 是否为 "AUTO_START"

**步骤 3**：通过导航到) 的已装载 ISO 中与 TAEF msi 相同的位置 (安装 WDTF，并为所需的体系结构安装包。 指定安装日志文件的位置和名称，在此示例中为 **%USERPROFILE%\Desktop\WDTFInstall.log** ：

```console
cd <ISO drive>\Program Files\Windows Kits\10\Testing\Runtimes
msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64_en-us.msi" /l* "%USERPROFILE%\Desktop\WDTFInstall.log"
```
WDTF MSI 将 WDTF 安装到 **%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\WDTF**。

**步骤 4**：配置计算机以进行测试：

1.  将计算机配置为收集完全转储或附加内核调试器。
2.  由于这些测试可能会重新启动计算机并需要控制睡眠周期，因此请将计算机配置为从不睡眠、从不关闭显示，并自动登录到测试帐户 ( # A0) 。  请注意，应谨慎使用自动登录。

**步骤 5**：通过将** \<ISO drive> \Program Files\Windows Kits\10\Testing\Tests\Additional Tests\x64\DevFund\DataDriven**中的所有文件复制到本地文件夹（例如 **%USERPROFILE%\Desktop\Tests**）来获取数据驱动的测试二进制文件。 卸载 ISO。