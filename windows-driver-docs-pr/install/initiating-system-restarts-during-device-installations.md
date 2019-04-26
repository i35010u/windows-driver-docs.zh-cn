---
title: 设备安装过程中开始系统重启
description: 设备安装过程中开始系统重启
ms.assetid: 52db2894-e759-4382-97de-5db7f268ff59
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a96876ac81b7b8fa15697588dfaebf4fc8debf1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325815"
---
# <a name="initiating-system-restarts-during-device-installations"></a>设备安装过程中开始系统重启


在极少数的情况下它是所需系统重新启动，以完成设备安装，请使用以下规则：

-   初始安装期间，设备的安装程序或辅助安装程序可以请求重新启动系统中设置 DI_NEEDRESTART [ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)结构，它收到的带有[设备安装函数代码](https://msdn.microsoft.com/library/windows/hardware/ff541307)。 (这不应完成除非绝对必要。)

-   更新安装期间，设备的安装应用程序可以调用[ **UpdateDriverForPlugAndPlayDevices**](https://msdn.microsoft.com/library/windows/hardware/ff553534)，用于确定是否需要重新启动系统。

 

 





