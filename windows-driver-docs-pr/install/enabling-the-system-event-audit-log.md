---
title: 启用系统事件审核日志
description: 启用系统事件审核日志
keywords:
- 详细日志记录 WDK 驱动程序签名
- 安全审核策略 WDK 驱动程序签名
- 系统审核策略 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc8305e4d244e71f5d311c2e516dee8dc118242
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813183"
---
# <a name="enabling-the-system-event-audit-log"></a>启用系统事件审核日志


本主题包括下列信息：

[如何启用安全审核策略](#how-to-enable-security-audit-policy)

[如何启用代码完整性诊断事件的详细日志记录](#how-to-enable-verbose-logging-of-code-integrity-diagnostic-events)

### <a name="how-to-enable-security-audit-policy"></a><a href="" id="how-to-enable-security-audit-policy"></a> 如何启用安全审核策略

若要启用安全审核策略来捕获审核日志中的加载失败，请执行以下步骤：

1.  打开提升的命令提示符窗口。 若要打开提升的命令提示符窗口，请创建 *Cmd.exe* 的桌面快捷方式，选择并按住 (或右键单击 *Cmd.exe* 快捷方式) ，然后选择 " **以管理员身份运行**"。

2.  在提升的命令提示符窗口中运行以下命令：

    ```cpp
    Auditpol /set /Category:System /failure:enable
    ```

3.  重新启动计算机以使更改生效。

以下屏幕截图显示了如何使用 Auditpol 启用安全审核。

![命令提示符窗口的屏幕截图，说明如何使用 auditpol 启用安全审核](images/driver-signing-enable-auditpol.png)

### <a name="how-to-enable-verbose-logging-of-code-integrity-diagnostic-events"></a><a href="" id="how-to-enable-verbose-logging-of-code-integrity-diagnostic-events"></a> 如何启用代码完整性诊断事件的详细日志记录

若要启用详细日志记录，请执行以下步骤：

1.  打开提升的命令提示符窗口。

2.  在命令行上运行 *Eventvwr.exe* 。

3.  在事件查看器左窗格中的 " **事件查看器** " 文件夹下，展开以下子文件夹序列：

    1.  **应用程序和服务日志**

    2.  **Microsoft**

    3.  **Windows**

4.  展开 " **Windows** " 文件夹下的 "**代码完整性**" 子文件夹，以显示其上下文菜单。

5.  选择 " **查看**"。

6.  选择 " **显示分析和调试日志**"。 然后事件查看器将显示一个包含 **操作** 文件夹和一个 **详细** 文件夹的子树。

7.  选择并按住 (或右键单击) **详细** "，然后从弹出上下文菜单中选择" **属性** "。

8.  选择 "**属性**" 对话框中的 "**常规**" 选项卡，然后选择属性页中间附近的 "**启用日志记录**" 选项。 这将启用详细日志记录。

9.  重新启动计算机以使更改生效。

 

 





