---
title: 将标记为具有执行完成安装操作的设备
description: 将标记为具有执行完成安装操作的设备
ms.assetid: 7f2560e6-94a7-4dd0-aa2a-e6cdd96c6d9b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d829f2eb41923ae6884f370bcfeb091adc12e114
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547505"
---
# <a name="marking-a-device-as-having-a-finish-install-action-to-perform"></a>将标记为具有执行完成安装操作的设备


*安装程序*（安装程序类、 类共同安装程序中或设备共同安装程序） 向指示 Windows 它已完成安装操作执行的安装程序在处理时设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702)请求。 此操作将导致 Windows 来标记该设备是无需执行完成安装操作。 步骤如下所示：

1.  当安装程序收到[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702)请求时，安装程序设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志，如果它具有要执行的完成安装操作。

    安装程序然后将返回以下错误代码之一：

    -   如果安装程序类安装程序完成安装向导并无网页，ERROR_DI_DO_DEFAULT。
    -   NO_ERROR 安装程序是否已完成安装向导页的类安装程序或具有或不具有完成安装向导页的共同安装程序。

2.  如果 DI_FLAGSEX_FINISHINSTALL_ACTION 标志设置的设备上处理完所有安装程序后[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702)设备，Windows 的请求标记的设备无需执行完成安装操作。

 

 





