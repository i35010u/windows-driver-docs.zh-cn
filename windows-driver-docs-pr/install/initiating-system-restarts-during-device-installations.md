---
title: 设备安装过程中开始系统重启
description: 设备安装过程中开始系统重启
ms.assetid: 52db2894-e759-4382-97de-5db7f268ff59
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc02c2773262d29759bd644709a61814fa6bb2b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370011"
---
# <a name="initiating-system-restarts-during-device-installations"></a>设备安装过程中开始系统重启


在极少数的情况下它是所需系统重新启动，以完成设备安装，请使用以下规则：

-   初始安装期间，设备的安装程序或辅助安装程序可以请求重新启动系统中设置 DI_NEEDRESTART [ **SP_DEVINSTALL_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)结构，它收到的带有[设备安装函数代码](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))。 (这不应完成除非绝对必要。)

-   更新安装期间，设备的安装应用程序可以调用[ **UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)，用于确定是否需要重新启动系统。

 

 





