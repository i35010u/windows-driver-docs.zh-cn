---
title: 在 Windows Vista 以前的操作系统中显示 UI
description: 在 Windows Vista 以前的操作系统中显示 UI
keywords:
- 打印后台处理程序自定义 WDK，Windows Vista 以前的 UI 显示
- 后台处理程序自定义 WDK 打印，Windows Vista 以前的 UI 显示
- 自定义打印后台处理程序组件 WDK，Windows Vista 以前的 UI 显示
- 显示打印组件的 UI
- 显示 WDK 打印的 UI
- 用户界面 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4506677fe640deb8df823a6d77a326670fe6a809
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797199"
---
# <a name="displaying-a-ui-in-operating-systems-prior-to-windows-vista"></a>在 Windows Vista 以前的操作系统中显示 UI





-   不要在后台处理程序的进程中运行的任何组件中显示 UI。

    后台处理程序在高特权安全级别运行;因此，显示 UI 会使后台处理程序成为恶意用户代码的风险。

-   检查驱动程序中的错误。

    Windows Vista 之前的操作系统版本中的异步通知调用失败。

-   使用 [**SplPromptUIInUsersSession**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-splpromptuiinuserssession) 函数显示简单对话框。

-   通过编写状态监视器显示复杂的用户界面元素。

    状态监视器是 IHV 开发和用户安装的应用程序。 由于状态监视器在用户的上下文中以用户的凭据运行，因此状态监视器可随时显示 UI 元素。 状态监视器可以使用双向通信或使用 TCPMON Xcv 接口与后台处理程序通信。 有关信息，请参阅 [添加双向通信](adding-bidirectional-communication.md) 和 [TCPMON Xcv 接口](tcpmon-xcv-interface.md)。

 

