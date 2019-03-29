---
title: 启用错误注入
description: 启用错误注入
ms.assetid: 451a5e9e-bc5c-4148-b475-7f38c535cf6a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78e47bd3171e3f0c05d8288962a6997010178e8b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568596"
---
# <a name="enabling-fault-injection"></a>启用错误注入


WdfTester 工具提供了一个 WMI 界面来配置特定的驱动程序 DDI 故障注入。 脚本 (WdftesterScript.wsf) 是前提是使用此 WMI 接口来配置错误注入。 您可以编写您自己的脚本，或使用提供的脚本以启用错误注入。 可以从命令提示符窗口，以注册、 配置和取消注册一个驱动程序运行的脚本 (WdftesterScript.wsf)。 该脚本还具有一个名为的命令行选项**runtest**。

### <a name="span-idwhattheruntestoptiondoesspanspan-idwhattheruntestoptiondoesspanwhat-the-runtest-option-does"></a><span id="what_the_runtest_option_does"></span><span id="WHAT_THE_RUNTEST_OPTION_DOES"></span>Runtest 选项的作用

**Runtest**选项执行简单禁用和启用驱动程序上的操作。 此选项将演示如何使用该工具。 首先，该脚本将禁用指定的驱动程序，然后再启用它。 这允许 WdfTester 监视在禁用期间所做的所有 DDI 调用并启用操作。 该脚本使用 WMI 接口之一来获取在此期间调用的 DDIs 列表。 此脚本确定 （仅这些，返回 NTSTATUS） 可能失败的这些 DDIs。 该脚本然后调用另一个 WMI 接口来配置 WdfTester 失败列表中的第一个 DDI。 该脚本禁用，并且使该驱动程序，这会导致 DDI 失败并引发 WMI 事件。 该脚本已等待 WMI 失败事件上 DDI。 如果已成功接收到事件和失败没有导致计算机停止响应或导致的 bug 检查 （这是由驱动程序开发人员或测试） 测试仍被视为成功。 然后，该脚本的列表中的下一步 DDI 重复这些步骤。

**请注意**   **runtest**选项要求你复制[DevCon](devcon.md) (Devcon.exe) 工具，然后将其放在与其他 Wdftester 文件相同的目录。 Devcon.exe 应用程序位于 *%wdkroot%*\\工具\\*&lt;平台&gt;* 目录。

 

**Runtest 选项中：**

1.  向 WdfTester 注册您的驱动程序。 如果尚未安装您的驱动程序，则必须使用 runtest 之前安装它。

2.  启用此驱动程序的驱动程序验证程序 (运行 Windows Vista 的计算机或更高版本不需要重新启动)。

3.  禁用驱动程序，通过使用 Devcon 应用程序。

4.  通过使用 Devcon 应用程序，驱动程序。

5.  检索的函数的调用期间启用和禁用操作并标识返回可能失败 NTSTATUS 和的这些函数的名称。

6.  启动异步 WMI 事件通知。

7.  对于每个 DDI 的可以从在步骤 5 中获取的列表失败：
    1.  配置失败的函数。
    2.  禁用，然后使用 Devcon.exe，驱动程序。 此操作将调用函数，并且 WdfTester 失败的函数调用。
    3.  等待要激发的 WMI 事件。
    4.  如果触发 WMI 事件时， **runtest**选项重复步骤 7 的列表中的下一个函数。

8.  取消注册该驱动程序。

 

 





