---
title: VM 交换机验证
description: VM 交换机验证选项监视在 Hyper-v 可扩展交换机内运行)  (可扩展交换机扩展的筛选器驱动程序。 使用此选项可以捕获在可扩展交换机内的 send 或 receive 操作中发生的错误。
ms.assetid: 629C0C70-D6C6-4977-A36B-6BD6EEC14FE8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96a72932fbda062486ad20f6c281e56d4e1b75fc
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381755"
---
# <a name="vm-switch-verification"></a>VM 交换机验证


VM 交换机验证选项监视在[Hyper-v 可扩展交换机](../network/hyper-v-extensible-switch.md)内运行)  (*可扩展交换机扩展*的筛选器驱动程序。 使用此选项可以捕获在可扩展交换机内的 send 或 receive 操作中发生的错误。

**注意**   此选项可从 Windows 8.1 开始使用。

 

如果此选项处于活动状态，则驱动程序验证程序将发出 [**Bug 检查 0xC4**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突) 如果可扩展交换机扩展无法正确地调用 hyper-v 可扩展交换机处理程序函数。

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活 VM 交换机验证功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用 Power Framework 延迟模糊化选项。

-   **在命令行中**

    在命令行中，VM 交换机验证由 **verifier/flags 0x01000000** (位 24) 表示。 若要激活 Power Framework 延迟模糊功能，请使用0x01000000 的标志值或将0x01000000 添加到标志值。 例如：

    ```
    verifier /flags 0x01000000  /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置") ** ，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查) **VM 交换机验证**。
    5.  重新启动计算机。

 

