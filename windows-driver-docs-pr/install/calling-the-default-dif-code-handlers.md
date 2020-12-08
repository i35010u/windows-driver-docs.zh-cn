---
title: 调用默认 DIF 代码处理程序
description: 调用默认 DIF 代码处理程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d023e7e1dcda57671437ebbd39da1b13b53aab40
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827977"
---
# <a name="calling-the-default-dif-code-handlers"></a>调用默认 DIF 代码处理程序


默认的 DIF 代码处理程序为 [DIF 代码](/previous-versions//ff541307(v=vs.85))执行系统定义的默认操作。 如 [处理 Dif 代码](handling-dif-codes.md)中所述，在 *类安装* 程序和 *共同安装程序* 首次处理了 dif 请求后， [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller)将调用一个 dif 请求的默认处理程序，但在 SetupDiCallClassInstaller 之前，在 **SetupDiCallClassInstaller** 之前，会回调为请求后处理而注册的共同安装程序。

**注意**  无法将 **SetupDiCallClassInstaller** 的操作配置为重新调用类安装程序来处理 DIF 请求。

 

在调用默认处理程序后， *类安装* 程序必须为某个 DIF 请求执行操作，在这种情况下，类安装程序必须在处理 dif 请求时直接调用默认处理程序，如下所示：

1.  执行必须在调用默认处理程序之前完成的操作。

2.  调用默认处理程序以执行默认操作。

    **注意**   类安装程序不得尝试取代默认处理程序的操作。

     

3.  执行必须在默认处理程序返回后执行的操作。

4.  如果类安装程序成功完成了对 DIF 请求的处理，则返回 NO_ERROR; 如果处理失败，则返回 Win32 错误。

**重要** 的 [共同安装](writing-a-co-installer.md)[程序和设备安装应用程序](writing-a-device-installation-application.md)不得调用默认的 DIF 代码处理程序。  

 

有关必须使用此方法的情况的示例，请参阅 [**DIF_INSTALLDEVICE**](./dif-installdevice.md)请求引用 "页上有关调用默认处理程序 [**SetupDiInstallDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiinstalldevice)的信息。

下表列出了具有默认处理程序的 DIF 代码。

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

 

