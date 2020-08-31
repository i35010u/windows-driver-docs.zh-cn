---
title: 辅助安装程序功能
description: 辅助安装程序功能
ms.assetid: ce8a5ab4-d5ce-4255-a959-9619ff736e37
keywords:
- 共同安装程序 WDK 设备安装，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5853c1db1b0fb94d839f6c06d835e79732f3931d
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094923"
---
# <a name="co-installer-functionality"></a>辅助安装程序功能





共同安装程序是一种用户模式 Win32 DLL，通常会将额外的配置信息写入注册表，或者执行其他安装任务，这些任务需要在写入 INF 时不可用的信息。

共同安装程序可能会执行以下部分或全部操作：

-   处理由[共同安装程序入口点](co-installer-interface.md#co-installer-entry-point)函数接收)  (DIF 代码的一个或多个[设备安装函数代码](/previous-versions/ff541307(v=vs.85))。

-   如 [共同安装程序操作](co-installer-operation.md)中所述，在调用类或设备安装程序之前或//之后，在调用关联的类或设备安装程序之前执行操作。

-   提供设备管理器显示的[设备属性页](providing-device-property-pages.md)，以便用户可以修改设备参数。

-   从 Windows Vista 开始，提供 ([安装操作](finish-install-actions--windows-vista-and-later-.md) ，以响应 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求) 安装应用程序。

为后处理而调用时，共同安装程序必须检查[COINSTALLER_CONTEXT_DATA](co-installer-interface.md#coinstaller-context-data)结构的**InstallResult**成员。 如果其值不 NO_ERROR，则共同安装程序必须执行任何必要的清理操作，并为 **InstallResult**返回相应的值。

共同安装程序有时可以从用户那里获取信息。 此类信息可能包括其他设备参数，或用户是否想要安装设备特定的应用程序。 共同安装程序可通过提供 "完成安装" 页和设备属性页来创建用户界面。 不允许使用其他形式的用户界面。 在安装结束时，Windows 将在安装结束时显示 "完成安装" 页 () 。 设备管理器显示属性页，并允许具有管理员权限的用户修改这些页上显示的参数。

 

