---
title: 在 Windows Vista 以前的操作系统中显示 UI
description: 在 Windows Vista 以前的操作系统中显示 UI
ms.assetid: de62310e-b10a-49b0-9bcc-b918318b2728
keywords:
- 打印后台处理程序自定义 WDK，早于 Windows Vista UI 显示
- 自定义 WDK 打印，早于 Windows Vista 用户界面显示的后台处理程序
- 自定义打印后台处理程序组件 WDK，早于 Windows Vista UI 显示
- 打印组件显示 UI
- UI 显示 WDK 打印
- 用户界面 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 970e0ea9559bdafb3be6b48d42977d4667624768
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370943"
---
# <a name="displaying-a-ui-in-operating-systems-prior-to-windows-vista"></a>在 Windows Vista 以前的操作系统中显示 UI





-   在后台处理程序的进程中运行任何组件中不显示 UI。

    在高特权安全级别; 上运行后台处理程序因此，显示用户界面将打开恶意用户代码的风险的后台处理程序。

-   检查驱动程序中的错误。

    在 Windows Vista 之前的操作系统版本中，异步通知调用失败。

-   通过显示简单的对话框[ **SplPromptUIInUsersSession** ](https://msdn.microsoft.com/library/windows/hardware/ff562679)函数。

-   通过编写状态监视器显示复杂的用户界面元素。

    状态监视器是 IHV 开发并且在用户安装的应用程序。 由于用户的凭据的用户的上下文中运行的状态监视器，因此是安全的状态监视器以在任何时候显示 UI 元素。 使用双向通信，或使用 TCPMON Xcv 界面，可与后台处理程序通信状态监视器。 有关信息，请参阅[添加双向通信](adding-bidirectional-communication.md)并[TCPMON Xcv 接口](tcpmon-xcv-interface.md)。

 

 




