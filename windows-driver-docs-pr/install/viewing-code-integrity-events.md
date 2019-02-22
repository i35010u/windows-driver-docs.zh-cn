---
title: 查看代码完整性事件
description: 查看代码完整性事件
ms.assetid: b1c8ea3e-1a10-41fd-bdc8-c1e6e7344d39
keywords:
- 事件查看器 WDK 驱动程序签名
- 查看代码完整性事件
- 显示代码完整性事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d603f1f72a0b30a217fb9c277dc0e0c159f4cf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547461"
---
# <a name="viewing-code-integrity-events"></a>查看代码完整性事件


可以使用事件查看器查看代码完整性事件。 您可以访问事件查看器中的计算机管理 Microsoft 管理控制台 (MMC) 一起或通过运行*Eventvwr.exe*命令从命令行。

若要查看事件查看器中的代码完整性事件，请展开以下一系列子文件夹下**事件查看器**计算机管理 MMC 或事件查看器窗口的左窗格中的文件夹：

1.  **应用程序和服务日志**

2.  **Microsoft**

3.  **Windows**

4.  **CodeIntegrity**

下面的屏幕截图显示了扩展的结果**CodeIntegrity**下的子文件夹**事件查看器**文件夹。

![说明如何查看计算机管理窗口的屏幕截图完整性事件编写代码](images/signing-code-integrity-folder.png)

对于特定的代码完整性日志条目有关的详细信息，右键单击该条目，然后选择**事件属性**上弹出菜单。 下面的屏幕截图显示了代码完整性事件的详细信息。

![事件属性对话框，说明未签名驱动程序错误的屏幕截图](images/event-prop.png)

此事件表示，Toaster 驱动程序 (toaster.sys) 无法加载，因为它是无符号 （或尝试加载 toaster.sys 映像不是同一个已由发布者进行数字签名）。

所有代码完整性事件日志消息的列表，请参阅[代码完整性事件日志消息](code-integrity-event-log-messages.md)。

系统日志事件是可以看到，在事件查看器在 Windows 日志、 系统日志视图。

 

 





