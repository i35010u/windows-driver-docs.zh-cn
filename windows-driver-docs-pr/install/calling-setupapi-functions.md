---
title: 调用 SetupAPI 函数
description: 调用 SetupAPI 函数
ms.assetid: 757AAF33-B57B-4ab8-A034-23B8AC0C5CB3
keywords:
- 安装程序 Api 函数 WDK 中，使用调用
- 调用安装程序 Api 函数 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ad0cbe865e850a35185ff994e996b5163736ab8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575447"
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
| [**DIF_PROPERTYCHANGE**](https://msdn.microsoft.com/library/windows/hardware/ff543712)                | [**SetupDiChangeState**](https://msdn.microsoft.com/library/windows/hardware/ff550930)                               |
| [**DIF_FINISHINSTALL_ACTION**](https://msdn.microsoft.com/library/windows/hardware/ff543684)   | [**SetupDiFinishInstallAction**](https://msdn.microsoft.com/library/windows/hardware/ff551022)               |
| [**DIF_INSTALLDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff543692)                  | [**SetupDiInstallDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552039)                           |
| [**DIF_INSTALLINTERFACES**](https://msdn.microsoft.com/library/windows/hardware/ff543695)          | [**SetupDiInstallDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff552043)       |
| [**DIF_INSTALLDEVICEFILES**](https://msdn.microsoft.com/library/windows/hardware/ff543694)        | [**SetupDiInstallDriverFiles**](https://msdn.microsoft.com/library/windows/hardware/ff552048)                 |
| [**DIF_REGISTER_COINSTALLERS**](https://msdn.microsoft.com/library/windows/hardware/ff543715) | [**SetupDiRegisterCoDeviceInstallers**](https://msdn.microsoft.com/library/windows/hardware/ff552085) |
| [**DIF_REGISTERDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff543713)                | [**SetupDiRegisterDeviceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff552091)                 |
| [**DIF_REMOVE**](https://msdn.microsoft.com/library/windows/hardware/ff543717)                                | [**SetupDiRemoveDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552097)                             |
| [**DIF_SELECTBESTCOMPATDRV**](https://msdn.microsoft.com/library/windows/hardware/ff543719)      | [**SetupDiSelectBestCompatDrv**](https://msdn.microsoft.com/library/windows/hardware/ff552112)               |
| [**DIF_SELECTDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff543723)                    | [**SetupDiSelectDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552115)                             |
| [**DIF_UNREMOVE**](https://msdn.microsoft.com/library/windows/hardware/ff543728)                            | [**SetupDiUnremoveDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552193)                         |

 

 

 





