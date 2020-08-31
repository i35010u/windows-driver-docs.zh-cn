---
title: 调用默认 DIF 代码处理程序
description: 调用默认 DIF 代码处理程序
ms.assetid: bc168c30-2269-4760-bc0a-e3e6ee3ce720
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ddbeda1772882a21ed6b6de8771b14baeaa3081
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094929"
---
# <a name="calling-the-default-dif-code-handlers"></a>调用默认 DIF 代码处理程序


默认的 DIF 代码处理程序为 DIF 代码执行系统定义的默认操作，并且 *共同安装程序* 首先处理了 dif 请求，但在 **SetupDiCallClassInstaller** 之前，请先处理已注册用于请求后处理的共同安装程序。

**注意**   无法将**SetupDiCallClassInstaller**的操作配置为重新调用类安装程序来处理 DIF 请求。

 

在调用默认处理程序后， *类安装* 程序必须为某个 DIF 请求执行操作，在这种情况下，类安装程序必须在处理 dif 请求时直接调用默认处理程序，如下所示：

1.  执行必须在调用默认处理程序之前完成的操作。

2.  调用默认处理程序以执行默认操作。

    **注意**   类安装程序不得尝试取代默认处理程序的操作。

     

3.  执行必须在默认处理程序返回后执行的操作。

4.  如果类安装程序成功完成了对 DIF 请求的处理，则返回 NO_ERROR; 如果处理失败，则返回 Win32 错误。

**重要**的  [共同安装](writing-a-co-installer.md)[程序和设备安装应用程序](writing-a-device-installation-application.md)不得调用默认的 DIF 代码处理程序。

 

有关必须使用此方法的情况的示例，请参阅[**DIF_INSTALLDEVICE**](./dif-installdevice.md)请求引用 "页上有关调用默认处理程序[**SetupDiInstallDevice**](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)的信息。

下表列出了具有默认处理程序的 DIF 代码。

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

 

 

