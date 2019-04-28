---
title: 启用代码完整性事件日志记录和系统审核
description: 介绍如何启用代码完整性事件日志记录和审核系统。
ms.assetid: D17C64F1-B295-4EC1-B0D0-F1A119D77F64
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa5f52d76a41d18bda2c3d1de153f86a901b5a1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342008"
---
# <a name="appendix-3-enable-code-integrity-event-logging-and-system-auditing"></a>附录 3：启用代码完整性事件日志记录和系统审核


## <a name="enable-code-integrity-event-logging-and-system-auditing"></a>启用代码完整性事件日志记录和系统审核


*从节选*[代码完整性事件日志记录和审核系统](enabling-code-integrity-event-logging-and-system-auditing.md):

代码完整性是内核模式组件，用于实现驱动程序签名验证。 它生成与映像验证相关的系统事件，并在代码完整性日志中记录信息：

-   代码完整性运行日志视图仅显示映像验证错误的事件。

-   代码完整性详细日志视图显示成功的签名验证的事件。

以下过程演示如何启用代码完整性详细事件日志记录，若要查看所有成功的操作系统加载程序和内核模式映像验证事件：

## <a name="to-enable-code-integrity-verbose-event-logging"></a>若要启用代码完整性详细事件日志记录


*从节选*[启用系统事件的审核日志](enabling-the-system-event-audit-log.md):

若要启用详细日志记录，请执行以下步骤：

1.  打开提升的命令提示符窗口。

2.  运行*Eventvwr.exe*命令行上。

3.  下**事件查看器**文件夹中的事件查看器中，左窗格中展开以下一系列子文件夹：

    1.  **应用程序和服务日志**

    2.  **Microsoft**

    3.  **Windows**

4.  展开**代码完整性**下的子文件夹**Windows**文件夹以显示其上下文菜单。

5.  选择**视图**。

6.  选择**显示分析和调试日志**。 事件查看器将显示包含的子树**Operational**文件夹和一个**Verbose**文件夹。

7.  右键单击**Verbose** ，然后选择**属性**弹出上下文菜单中。

8.  选择**常规**选项卡上**属性**对话框中，并选择**启用日志记录**中间附近的属性页的选项。 这将启用详细日志记录。

9.  重新启动计算机，更改才能生效。

系统事件记录还可以启用，其中包括代码完整性映像验证失败事件。 Windows 内核加载驱动程序，因为签名失败而失败时生成这些事件。 代码完整性操作事件日志视图中也会记录类似事件

## <a name="to-enable-the-audit-policy-to-generate-audit-events-in-the-system-category-for-failed-operations"></a>若要启用中失败的操作的系统类别生成审核事件的审核策略


若要启用安全审核策略，以捕获在审核日志中的加载失败，请执行以下步骤：

1.  打开提升的命令提示符窗口。 若要打开提升的命令提示符窗口，请创建桌面快捷方式*Cmd.exe*，右键单击*Cmd.exe*快捷方式，然后选择**以管理员身份运行**。

2.  在提升的命令提示符窗口中，运行以下命令：

    ```cpp
    Auditpol /set /Category:System /failure:enable
    ```

3.  重新启动计算机，更改才能生效。

下面的屏幕截图显示一个如何使用 Auditpol 启用安全审核。

![说明如何使用 auditpol 启用安全审核的命令提示符窗口的屏幕截图](images/tutorialauditpol.jpg)

 

 





