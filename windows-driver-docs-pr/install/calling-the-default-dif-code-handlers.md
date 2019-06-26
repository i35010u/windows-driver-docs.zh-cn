---
title: 调用默认 DIF 代码处理程序
description: 调用默认 DIF 代码处理程序
ms.assetid: bc168c30-2269-4760-bc0a-e3e6ee3ce720
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb1987eb32b093cde2520b7c33714bc6fd3c3b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385284"
---
# <a name="calling-the-default-dif-code-handlers"></a>调用默认 DIF 代码处理程序


默认 DIF 代码处理程序执行系统定义的默认操作为 DIF 代码和*共同安装程序*先处理完 DIF 请求之前**SetupDiCallClassInstaller**召回注册以便进行后续处理的请求的共同安装程序。

**请注意**  的操作**SetupDiCallClassInstaller**不能配置可用于召回类安装程序进行后处理 DIF 请求。

 

在这些情况下，*类安装程序*必须执行的操作差异请求调用默认处理程序后，类安装程序必须直接调用默认处理程序，如下所示处理 DIF 请求时：

1.  执行之前调用默认处理程序都必须执行的操作。

2.  调用默认处理程序执行默认操作。

    **请注意**  类安装程序不能尝试取代默认处理程序的操作。

     

3.  执行默认处理程序返回后必须完成的操作。

4.  如果类安装程序成功完成处理 DIF 请求返回 NO_ERROR 或如果处理失败，则返回一个 Win32 错误。

**重要**  [共同安装程序](writing-a-co-installer.md)并[设备安装应用程序](writing-a-device-installation-application.md)DIF 代码处理程序不能调用默认值。

 

必须使用此方法的位置的情况的示例，请参阅有关调用默认处理程序的信息[ **SetupDiInstallDevice** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)上[ **DIF_INSTALLDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice)请求参考页。

下表列出了具有默认处理程序的差异代码。

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

 

 

 





