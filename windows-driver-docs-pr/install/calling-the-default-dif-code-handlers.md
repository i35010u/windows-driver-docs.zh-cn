---
title: 调用默认 DIF 代码处理程序
description: 调用默认 DIF 代码处理程序
ms.assetid: bc168c30-2269-4760-bc0a-e3e6ee3ce720
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c67142d1b5f71d813c1df651d42f56fb8702986
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374309"
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

 

必须使用此方法的位置的情况的示例，请参阅有关调用默认处理程序的信息[ **SetupDiInstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552039)上[ **DIF_INSTALLDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff543692)请求参考页。

下表列出了具有默认处理程序的差异代码。

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

 

 

 





