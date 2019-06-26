---
title: 辅助安装程序功能
description: 辅助安装程序功能
ms.assetid: ce8a5ab4-d5ce-4255-a959-9619ff736e37
keywords:
- 共同安装程序 WDK 设备安装功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1bbc054ecd43c6b63d95a3e48c395c11c9bc1b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375335"
---
# <a name="co-installer-functionality"></a>辅助安装程序功能





辅助安装程序是一个用户模式 Win32 DLL，它通常将额外的配置信息写入到注册表中，或执行其他安装任务的需要写入 INF 时不可用的信息。

辅助安装程序可能会执行部分或全部以下操作：

-   处理一个或多个[设备安装函数代码](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))（DIF 代码） 收到[共同安装程序入口点](co-installer-interface.md#co-installer-entry-point)函数。

-   执行操作之前调用关联的类或设备安装程序时后调用的类或设备安装程序，还是两者，如中所述[共同安装程序操作](co-installer-operation.md)。

-   [提供设备属性页](providing-device-property-pages.md)，其中显示设备管理器，以便用户可以修改设备参数。

-   从 Windows Vista 开始提供[完成安装操作](finish-install-actions--windows-vista-and-later-.md)(在响应[ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)请求) 以安装应用程序。

辅助安装程序时调用的后续处理，必须检查**InstallResult**的成员[COINSTALLER_CONTEXT_DATA](co-installer-interface.md#coinstaller-context-data)结构。 如果其值不为 NO_ERROR，辅助安装程序必须执行所有必需清理操作并返回适当的值**InstallResult**。

有时，共同安装程序可以从用户获取信息。 此类信息可能包括其他设备参数，或用户是否希望安装的特定于设备的应用程序。 共同安装程序可以通过提供"完成安装"页和设备属性页创建用户界面。 不允许任何其他形式的用户界面。 Windows （在发现新硬件或硬件更新） 安装结束时显示"完成安装"页。 设备管理器中显示属性页中，并允许具有管理员权限的用户修改这些页面上显示的参数。

 

 





