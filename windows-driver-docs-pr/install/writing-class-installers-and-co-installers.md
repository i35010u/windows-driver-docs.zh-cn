---
title: 编写类安装程序和辅助安装程序
description: 编写类安装程序和辅助安装程序
ms.assetid: DA52A2C4-81D7-4e95-97CD-D5A1C625CE02
keywords:
- 类安装程序 WDK 设备安装编写
- 编写 WDK 设备安装的安装程序类
- 编写的共同安装程序 WDK 设备安装
- 编写 WDK 设备安装的共同安装程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0337a4062121a78ad9f2616f4713986842d683e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363476"
---
# <a name="writing-class-installers-and-co-installers"></a>编写类安装程序和辅助安装程序


**请注意**  通用或移动设备的驱动程序包中不支持在本部分中所述的功能。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

本部分包含在编写时应遵循的准则*共同安装程序*:

[显示用户界面](#displaying-a-user-interface)

[正在保存设备安装状态](#saving-device-installation-state)

[正在加载可执行文件或 DLL 文件](#loading-executable-or-dll-files)

[启动其他进程或服务](#starting-other-processes-or-services)

有关如何编写共同安装程序的详细信息，请参阅[编写共同安装程序](writing-a-co-installer.md)。

## <a name="displaying-a-user-interface"></a>显示用户界面


设备安装通常在系统 （非交互式） 服务中运行。 因此，用户无法查看或响应将显示在此上下文中任何用户界面。 中提供任何对话框*共同安装程序*的处理过程[设备安装函数 (DIF) 代码](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))，设备安装程序将停止响应。

在大多数情况下，共同安装程序应该不与用户交互除外的处理期间[完成安装操作](finish-install-actions--windows-vista-and-later-.md)。 完成安装操作在交互式上下文中运行。

**请注意**  共同安装程序应无法与 ERROR_REQUIRES_INTERACTIVE_WINDOWSTATION DIF 代码，因为这将导致设备安装失败。 如果设备安装需要用户交互，共同安装程序应支持完成安装操作。

 

## <a name="saving-device-installation-state"></a>正在保存设备安装状态


不保存在设备安装状态*共同安装程序*动态链接库 (DLL)。 因为 DIF 代码处理由安装程序后，Windows 通常会卸载该 DLL，将不会保留在 DLL 内保存任何状态信息。

若要安全地保留设备安装程序状态，类安装程序或共同安装程序应该将保存的状态信息为中设备的属性*驱动程序键*注册表中。 要实现这一点，请执行下列操作：

1.  若要检索的注册表句柄的驱动程序键*设备实例*，使用[ **SetupDiOpenDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)与*KeyType*参数将设置为 DIREG_DRV。

2.  使用[ **SetupDiGetDevicePropertyKeys** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys) （若要检索的设备实例的所有属性密钥） 或[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)（用于检索指定的设备实例属性键）。

3.  使用[ **SetupDiSetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)保存设备实例属性键。

## <a name="loading-executable-or-dll-files"></a>正在加载可执行文件或 DLL 文件


如果你*共同安装程序*尝试在 Windows 64 位平台上，操作系统加载未签名的可执行文件或 DLL 防止它被加载在此安全环境中。

若要安全地加载可执行文件或 DLL 的类安装程序或辅助安装程序，我们强烈建议的可执行文件或 DLL 不包含在数字签名[驱动程序包](driver-packages.md)。 有关如何签署驱动程序包的详细信息，请参阅[驱动程序签名](driver-signing.md)。

**请注意**  类安装程序和共同安装程序不能通过加载 DLL 模块显式函数调用，如**LoadLibrary**，或通过创建链接的依赖项。

 

## <a name="starting-other-processes-or-services"></a>启动其他进程或服务


设备在安装期间，Windows 无法跟踪其他进程，并且不能以确定它们执行的操作或如果它们没有完成。 例如，Windows 无法启动或停止设备或进程正在执行关键操作时开始系统重启。

在大多数情况下，*共同安装程序*应启动其他进程或服务。 但是，安装程序可以启动其他进程安全地通过调用[CreateProcess](https://go.microsoft.com/fwlink/p/?linkid=194524)从函数或通过显示的对话框[完成安装操作](finish-install-actions--windows-vista-and-later-.md)。 安装程序必须允许用户继续对话框或过程中，直到创建的进程已退出。

 

 





