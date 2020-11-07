---
title: 调用 SetupAPI 函数
description: 调用 SetupAPI 函数
ms.assetid: 757AAF33-B57B-4ab8-A034-23B8AC0C5CB3
keywords:
- Setupapi.log 函数 WDK，调用
- 调用 Setupapi.log 函数 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca3a240540ce0dd85448be3e2509def595afa6d2
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361285"
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

    **注意** 仅当在 *Flags* 参数中设置 SPQ_SCAN_PRUNE_COPY_QUEUE 标志时，才禁止类安装程序和共同安装程序调用 **SetupScanFileQueue** 。

     

### <a name="rules-for-calling-the-default-dif-code-handler-functions"></a><a href="" id="calling-the-default-dif-code-handler-functions"></a>调用默认的 DIF 代码处理函数的规则

默认 [设备安装函数 (dif) 代码](/previous-versions//ff541307(v=vs.85)) 处理程序函数为某些 DIF 代码执行系统定义的默认操作。 如 [处理 Dif 代码](handling-dif-codes.md)中所述，在 *共同安装程序* 首次处理了 dif 请求后， [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller)将调用一个 dif 请求的默认处理程序，但在 **SetupDiCallClassInstaller** 之前，将调用注册为请求后处理的共同安装程序。

[共同安装](writing-a-co-installer.md) 程序和 [设备安装应用程序](writing-a-device-installation-application.md) 不得调用默认的 DIF 代码处理程序函数。 直接调用这些处理程序函数将跳过所有已注册的共同安装程序，并且可能会使这些安装程序存储的任何内部设备状态无效。

下表列出了具有默认的 DIF 代码处理程序函数的 DIF 代码。

| DIF 代码                                                             | 默认的 DIF 代码处理程序函数                                                  |
|----------------------------------------------------------------------|------------------------------------------------------------------------------------|
| [**DIF_PROPERTYCHANGE**](./dif-propertychange.md)                | [**SetupDiChangeState**](/windows/win32/api/setupapi/nf-setupapi-setupdichangestate)                               |
| [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md)   | [**SetupDiFinishInstallAction**](/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85))               |
| [**DIF_INSTALLDEVICE**](./dif-installdevice.md)                  | [**SetupDiInstallDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiinstalldevice)                           |
| [**DIF_INSTALLINTERFACES**](./dif-installinterfaces.md)          | [**SetupDiInstallDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)       |
| [**DIF_INSTALLDEVICEFILES**](./dif-installdevicefiles.md)        | [**SetupDiInstallDriverFiles**](/windows/win32/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)                 |
| [**DIF_REGISTER_COINSTALLERS**](./dif-register-coinstallers.md) | [**SetupDiRegisterCoDeviceInstallers**](/windows/win32/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers) |
| [**DIF_REGISTERDEVICE**](./dif-registerdevice.md)                | [**SetupDiRegisterDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)                 |
| [**DIF_REMOVE**](./dif-remove.md)                                | [**SetupDiRemoveDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiremovedevice)                             |
| [**DIF_SELECTBESTCOMPATDRV**](./dif-selectbestcompatdrv.md)      | [**SetupDiSelectBestCompatDrv**](/windows/win32/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)               |
| [**DIF_SELECTDEVICE**](./dif-selectdevice.md)                    | [**SetupDiSelectDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiselectdevice)                             |
| [**DIF_UNREMOVE**](./dif-unremove.md)                            | [**SetupDiUnremoveDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiunremovedevice)                         |

 

