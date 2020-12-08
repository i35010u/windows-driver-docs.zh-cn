---
title: 查看代码完整性事件
description: 查看代码完整性事件
keywords:
- 事件查看器 WDK 驱动程序签名
- 查看代码完整性事件
- 显示代码完整性事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 490616aa544deeef9481929226501a4c4bf91c23
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840041"
---
# <a name="viewing-code-integrity-events"></a>查看代码完整性事件


您可以使用事件查看器查看代码完整性事件。 你可以在计算机管理 Microsoft 管理控制台 (MMC) 或通过从命令行运行 *Eventvwr.exe* 命令来访问事件查看器。

若要查看事件查看器中的代码完整性事件，请在 "计算机管理" MMC 或 "事件查看器" 窗口的左窗格中展开 " **事件查看器** " 文件夹下的以下子文件夹序列：

1.  **应用程序和服务日志**

2.  **Microsoft**

3.  **Windows**

4.  **CodeIntegrity**

以下屏幕截图显示了在 **事件查看器** 文件夹下展开 **CodeIntegrity** 子文件夹的结果。

!["计算机管理" 窗口的屏幕截图，演示如何查看代码完整性事件](images/signing-code-integrity-folder.png)

有关特定代码完整性日志条目的详细信息，请右键单击该条目，然后在弹出菜单中选择 " **事件属性** "。 下面的屏幕截图显示了有关代码完整性事件的详细信息。

![显示未签名驱动程序错误的 "事件属性" 对话框的屏幕截图](images/event-prop.png)

此事件表示无法加载 Toaster 驱动程序 ( # A0) ，因为它是无符号 (，或者尝试加载的 toaster.sys 映像与发布者) 进行了数字签名的图像不同。

有关所有代码完整性事件日志消息的列表，请参阅 [代码完整性事件日志消息](code-integrity-event-log-messages.md)。

系统日志事件可在 "Windows 日志"、"系统日志" 视图下的事件查看器中查看。

 

 





