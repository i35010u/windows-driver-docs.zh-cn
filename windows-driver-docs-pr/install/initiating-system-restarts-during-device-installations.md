---
title: 设备安装过程中开始系统重启
description: 设备安装过程中开始系统重启
ms.assetid: 52db2894-e759-4382-97de-5db7f268ff59
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a20f306e3df8d6469afda92ea4de82e5a1a0a0d9
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716356"
---
# <a name="initiating-system-restarts-during-device-installations"></a>设备安装过程中开始系统重启


在极少数情况下，系统需要重新启动才能完成设备安装，请使用以下规则：

-   在初始安装期间，设备的安装程序或共同安装程序可以通过在 [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a) 结构中设置 DI_NEEDRESTART 来请求系统重新启动，该结构随 [设备安装函数代码](/previous-versions/ff541307(v=vs.85))一起接收。  (除非绝对必要，否则不应执行此操作。 ) 

-   在更新安装过程中，设备的安装应用程序可以调用 [**UpdateDriverForPlugAndPlayDevices**](/windows/win32/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)，以确定是否需要重新启动系统。

 

