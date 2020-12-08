---
title: 设备安装过程中开始系统重启
description: 设备安装过程中开始系统重启
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0d4521c59b60a667684e295cb28f828a166b705
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813727"
---
# <a name="initiating-system-restarts-during-device-installations"></a>设备安装过程中开始系统重启


在极少数情况下，系统需要重新启动才能完成设备安装，请使用以下规则：

-   在初始安装期间，设备的安装程序或共同安装程序可以通过在 [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a) 结构中设置 DI_NEEDRESTART 来请求系统重新启动，该结构随 [设备安装函数代码](/previous-versions/ff541307(v=vs.85))一起接收。  (除非绝对必要，否则不应执行此操作。 ) 

-   在更新安装过程中，设备的安装应用程序可以调用 [**UpdateDriverForPlugAndPlayDevices**](/windows/win32/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)，以确定是否需要重新启动系统。

 

