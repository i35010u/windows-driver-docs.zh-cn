---
title: 调用 SetupAPI 函数
description: 调用 SetupAPI 函数
ms.assetid: 757AAF33-B57B-4ab8-A034-23B8AC0C5CB3
keywords:
- 安装程序 Api 函数 WDK 中，使用调用
- 调用安装程序 Api 函数 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b26c11d0c8b9fd35c83a50bdb7d3527267ff1775
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385286"
---
# <a name="calling-setupapi-functions"></a>调用 SetupAPI 函数


本部分提供了在调用时应遵循的准则[SetupAPI](setupapi.md)函数从[共同安装程序](writing-a-co-installer.md)或[设备安装应用程序](writing-a-device-installation-application.md)。

-   [调用安装程序 Api 函数的规则](#calling-setupapi-functions)
-   [调用 DIF 代码处理程序函数的默认规则](#calling-the-default-dif-code-handler-functions)

### <a href="" id="calling-setupapi-functions"></a>调用安装程序 Api 函数的规则

安装程序类和共同安装程序不能调用以下[SetupAPI](setupapi.md)函数：

-   **SetupQueueCopy**

-   **SetupQueueCopyIndirect**

-   **SetupQueueCopySection**

-   **SetupQueueDefaultCopy**

-   **SetupQueueDelete**

-   **SetupQueueDeleteSection**

-   **SetupQueueRename**

-   **SetupQueueRenameSection**

-   **SetupScanFileQueue**

    **请注意**  类的安装程序和共同安装程序禁止调用**SetupScanFileQueue**仅 SPQ_SCAN_PRUNE_COPY_QUEUE 标志设置*标志*参数。

     

### <a href="" id="calling-the-default-dif-code-handler-functions"></a>调用 DIF 代码处理程序函数的默认规则

默认设备安装函数 (DIF) 代码之前先处理 DIF 请求**SetupDiCallClassInstaller**调用注册共同安装程序以便进行后续处理的请求。

[共同安装程序](writing-a-co-installer.md)并[设备安装应用程序](writing-a-device-installation-application.md)DIF 代码处理程序函数不能调用默认值。 直接调用这些处理程序函数跳过所有已注册的共同安装程序，可能使这些安装程序存储任何内部设备状态无效。

下表列出了具有默认 DIF 代码处理程序函数的 DIF 代码。

| DIF 代码                                                             | 默认 DIF 代码处理程序函数                                                  |
|----------------------------------------------------------------------|------------------------------------------------------------------------------------|
| [**DIF_PROPERTYCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-propertychange)                | [**SetupDiChangeState**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate)                               |
| [**DIF_FINISHINSTALL_ACTION**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)   | [**SetupDiFinishInstallAction**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85))               |
| [**DIF_INSTALLDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice)                  | [**SetupDiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)                           |
| [**DIF_INSTALLINTERFACES**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installinterfaces)          | [**SetupDiInstallDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)       |
| [**DIF_INSTALLDEVICEFILES**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevicefiles)        | [**SetupDiInstallDriverFiles**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)                 |
| [**DIF_REGISTER_COINSTALLERS**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-register-coinstallers) | [**SetupDiRegisterCoDeviceInstallers**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers) |
| [**DIF_REGISTERDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-registerdevice)                | [**SetupDiRegisterDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)                 |
| [**DIF_REMOVE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-remove)                                | [**SetupDiRemoveDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)                             |
| [**DIF_SELECTBESTCOMPATDRV**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-selectbestcompatdrv)      | [**SetupDiSelectBestCompatDrv**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)               |
| [**DIF_SELECTDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-selectdevice)                    | [**SetupDiSelectDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice)                             |
| [**DIF_UNREMOVE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-unremove)                            | [**SetupDiUnremoveDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiunremovedevice)                         |

 

 

 





