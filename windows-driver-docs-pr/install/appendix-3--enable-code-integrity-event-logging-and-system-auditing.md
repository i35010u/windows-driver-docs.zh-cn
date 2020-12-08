---
title: 启用代码完整性事件日志记录和系统审核
description: 描述如何启用代码完整性事件日志记录和系统审核。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49ebff9ece4ff4b2a75c0ada2bfbb7d0a9b69b8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808181"
---
# <a name="appendix-3-enable-code-integrity-event-logging-and-system-auditing"></a>附录 3：启用代码完整性事件日志记录和系统审核


## <a name="enable-code-integrity-event-logging-and-system-auditing"></a>启用代码完整性事件日志记录和系统审核


*Excerpt from* [代码完整性事件日志记录和系统审核](enabling-code-integrity-event-logging-and-system-auditing.md)摘录：

代码完整性是实现驱动程序签名验证的内核模式组件。 它会生成与图像验证相关的系统事件，并将这些信息记录在代码完整性日志中：

-   代码完整性操作日志视图仅显示映像验证错误事件。

-   代码完整性详细日志视图显示成功签名验证的事件。

下面的过程演示如何启用代码完整性详细事件日志记录，以查看所有成功的操作系统加载程序和内核模式映像验证事件：

## <a name="to-enable-code-integrity-verbose-event-logging"></a>启用代码完整性详细事件日志记录


[启用系统事件审核日志](enabling-the-system-event-audit-log.md)*的摘录*：

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

7.  右键单击 " **详细** "，然后从弹出上下文菜单中选择 " **属性** "。

8.  选择 "**属性**" 对话框中的 "**常规**" 选项卡，然后选择属性页中间附近的 "**启用日志记录**" 选项。 这将启用详细日志记录。

9.  重新启动计算机以使更改生效。

还可以启用系统事件记录，其中包括代码完整性映像验证失败事件。 由于签名失败，Windows 内核无法加载驱动程序时，将生成这些事件。 类似事件也会记录在代码完整性操作事件日志视图中

## <a name="to-enable-the-audit-policy-to-generate-audit-events-in-the-system-category-for-failed-operations"></a>启用审核策略以在系统类别中为失败的操作生成审核事件


若要启用安全审核策略来捕获审核日志中的加载失败，请执行以下步骤：

1.  打开提升的命令提示符窗口。 若要打开提升的命令提示符窗口，请创建 *Cmd.exe* 的桌面快捷方式，右键单击 *Cmd.exe* 快捷方式，然后选择 " **以管理员身份运行**"。

2.  在提升的命令提示符窗口中运行以下命令：

    ```cpp
    Auditpol /set /Category:System /failure:enable
    ```

3.  重新启动计算机以使更改生效。

以下屏幕截图显示了如何使用 Auditpol 启用安全审核。

![命令提示符窗口的屏幕截图，说明如何使用 auditpol 启用安全审核](images/tutorialauditpol.jpg)

 

 





