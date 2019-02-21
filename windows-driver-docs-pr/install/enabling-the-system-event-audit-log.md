---
title: 启用系统事件的审核日志
description: 启用系统事件的审核日志
ms.assetid: a4206f06-0c81-407e-80aa-4f6b08cb2a70
keywords:
- 详细日志记录 WDK 驱动程序签名
- 安全审核策略 WDK 驱动程序签名
- 系统审核策略 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17628840a7d2bc6d7bda4d9399fa82b1c02fb4fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540444"
---
# <a name="enabling-the-system-event-audit-log"></a>启用系统事件的审核日志


本主题包括下列信息：

[如何启用安全审核策略](#how-to-enable-security-audit-policy)

[如何启用详细日志记录的代码完整性诊断事件](#how-to-enable-verbose-logging-of-code-integrity-diagnostic-events)

### <a href="" id="how-to-enable-security-audit-policy"></a> 如何启用安全审核策略

若要启用安全审核策略，以捕获在审核日志中的加载失败，请执行以下步骤：

1.  打开提升的命令提示符窗口。 若要打开提升的命令提示符窗口，请创建桌面快捷方式*Cmd.exe*，右键单击*Cmd.exe*快捷方式，然后选择**以管理员身份运行**。

2.  在提升的命令提示符窗口中，运行以下命令：

    ```cpp
    Auditpol /set /Category:System /failure:enable
    ```

3.  重新启动计算机，更改才能生效。

下面的屏幕截图显示一个如何使用 Auditpol 启用安全审核。

![说明如何使用 auditpol 启用安全审核的命令提示符窗口的屏幕截图](images/driver-signing-enable-auditpol.png)

### <a href="" id="how-to-enable-verbose-logging-of-code-integrity-diagnostic-events"></a> 如何启用详细日志记录的代码完整性诊断事件

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

 

 





