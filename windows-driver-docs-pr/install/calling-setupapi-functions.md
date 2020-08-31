---
title: 调用 SetupAPI 函数
description: 调用 SetupAPI 函数
ms.assetid: 757AAF33-B57B-4ab8-A034-23B8AC0C5CB3
keywords:
- Setupapi.log 函数 WDK，调用
- 调用 Setupapi.log 函数 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5b7e4731aa084758e2b120151b69ef74172dedb
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095763"
---
# <a name="calling-setupapi-functions"></a>调用 SetupAPI 函数


本部分提供从[共同安装](writing-a-co-installer.md)[程序或设备安装应用程序](writing-a-device-installation-application.md)调用[setupapi.log](setupapi.md)函数时应遵循的准则。

-   [调用 Setupapi.log 函数的规则](#calling-setupapi-functions)
-   [调用默认的 DIF 代码处理函数的规则](#calling-the-default-dif-code-handler-functions)

### <a name="rules-for-calling-setupapi-functions"></a><a href="" id="calling-setupapi-functions"></a>调用 Setupapi.log 函数的规则

类安装程序和共同安装程序不得调用以下 [setupapi.log](setupapi.md) 函数：

-   **SetupQueueCopy**

-   **SetupQueueCopyIndirect**

-   **SetupQueueCopySection**

-   **SetupQueueDefaultCopy**

-   **SetupQueueDelete**

-   **SetupQueueDeleteSection**

-   **SetupQueueRename**

-   **SetupQueueRenameSection**

-   **SetupScanFileQueue**

    **注意**   仅当在*Flags*参数中设置 SPQ_SCAN_PRUNE_COPY_QUEUE 标志时，才禁止类安装程序和共同安装程序调用**SetupScanFileQueue** 。

     

### <a name="rules-for-calling-the-default-dif-code-handler-functions"></a><a href="" id="calling-the-default-dif-code-handler-functions"></a>调用默认的 DIF 代码处理函数的规则

默认设备安装函数 (DIF) 代码首先处理了该 DIF 请求，但在 **SetupDiCallClassInstaller** 调用注册为请求后处理的共同安装程序之前。

[共同安装](writing-a-co-installer.md) 程序和 [设备安装应用程序](writing-a-device-installation-application.md) 不得调用默认的 DIF 代码处理程序函数。 直接调用这些处理程序函数将跳过所有已注册的共同安装程序，并且可能会使这些安装程序存储的任何内部设备状态无效。

下表列出了具有默认的 DIF 代码处理程序函数的 DIF 代码。

| DIF 代码                                                             | 默认的 DIF 代码处理程序函数                                                  |
|----------------------------------------------------------------------|------------------------------------------------------------------------------------|
| [**DIF_PROPERTYCHANGE**](./dif-propertychange.md)                | [**SetupDiChangeState**](/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate)                               |
| [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md)   | [**SetupDiFinishInstallAction**](/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85))               |
| [**DIF_INSTALLDEVICE**](./dif-installdevice.md)                  | [**SetupDiInstallDevice**](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)                           |
| [**DIF_INSTALLINTERFACES**](./dif-installinterfaces.md)          | [**SetupDiInstallDeviceInterfaces**](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)       |
| [**DIF_INSTALLDEVICEFILES**](./dif-installdevicefiles.md)        | [**SetupDiInstallDriverFiles**](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)                 |
| [**DIF_REGISTER_COINSTALLERS**](./dif-register-coinstallers.md) | [**SetupDiRegisterCoDeviceInstallers**](/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers) |
| [**DIF_REGISTERDEVICE**](./dif-registerdevice.md)                | [**SetupDiRegisterDeviceInfo**](/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)                 |
| [**DIF_REMOVE**](./dif-remove.md)                                | [**SetupDiRemoveDevice**](/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)                             |
| [**DIF_SELECTBESTCOMPATDRV**](./dif-selectbestcompatdrv.md)      | [**SetupDiSelectBestCompatDrv**](/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)               |
| [**DIF_SELECTDEVICE**](./dif-selectdevice.md)                    | [**SetupDiSelectDevice**](/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice)                             |
| [**DIF_UNREMOVE**](./dif-unremove.md)                            | [**SetupDiUnremoveDevice**](/windows/desktop/api/setupapi/nf-setupapi-setupdiunremovedevice)                         |

 

 

