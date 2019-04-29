---
title: 快速用户切换
description: 快速用户切换
ms.assetid: 79e13d56-f71f-4a7d-9069-de4821d29d94
keywords:
- 显示驱动程序模型 WDK Windows 2000，快速用户切换
- Windows 2000 显示器驱动程序模型 WDK，快速用户切换
- 微型端口驱动程序 WDK Windows 2000 中，快速用户切换
- 快速用户切换 WDK Windows 2000 显示
- 显示多个虚拟显示器驱动程序 WDK Windows 2000
- 显示的虚拟显示器驱动程序 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000，快速用户切换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba10c0cfff0b4b06e97f8af5476bb3e59a5f7b15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360731"
---
# <a name="fast-user-switching"></a>快速用户切换


## <span id="ddk_fast_user_switching_gg"></span><span id="DDK_FAST_USER_SWITCHING_GG"></span>


快速用户切换，一项功能的 Windows XP 及更高版本，使多个用户能够登录到同一台计算机上。 特定用户的桌面和任何正在运行的应用程序保存到他或她的下一步从该用户的登录会话。

快速用户切换工作原理是使多个虚拟显示器驱动程序在同一时间运行。 （每个虚拟显示器驱动程序是与特定 PDEV 相关联。）微型端口驱动程序，但是，存在为单一实例。 当其中一个的虚拟显示器驱动程序调用的微型端口驱动程序回调时，严重的问题会随之发生如果微型端口驱动程序尝试访问传入的内存地址显示驱动程序的上下文中，当该显示驱动程序实例不再处于活动状态内核线程。 显示驱动程序/视频微型端口驱动程序体系结构原则是信息应只在一个方向流动： 从显示器驱动程序微型端口驱动程序。

 

 





