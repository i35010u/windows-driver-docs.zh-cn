---
title: 编写类安装程序和辅助安装程序
description: 编写类安装程序和辅助安装程序
ms.assetid: DA52A2C4-81D7-4e95-97CD-D5A1C625CE02
keywords:
- 类安装程序 WDK 设备安装，编写
- 编写类安装程序 WDK 设备安装
- 共同安装程序 WDK 设备安装，编写
- 编写共同安装程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa4eb6395ae3b3cd239cc28ac6a6e9e4347dcb22
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097059"
---
# <a name="writing-class-installers-and-co-installers"></a>编写类安装程序和辅助安装程序


**注意**   通用或移动驱动程序包不支持本部分中介绍的功能。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

本部分包含编写 *共同安装程序*时应遵循的准则：

[显示用户界面](#displaying-a-user-interface)

[正在保存设备安装状态](#saving-device-installation-state)

[加载可执行文件或 DLL 文件](#loading-executable-or-dll-files)

[启动其他进程或服务](#starting-other-processes-or-services)

有关如何编写共同安装程序的详细信息，请参阅 [编写共同安装程序](writing-a-co-installer.md)。

## <a name="displaying-a-user-interface"></a>显示用户界面


设备安装主要在 (非交互式) 服务的系统中运行。 因此，用户无法查看或响应在此上下文中出现的任何用户界面。 在设备安装功能的 *处理过程中* 提供的任何对话框 [ (DIF) 代码](/previous-versions/ff541307(v=vs.85)) 会导致设备安装停止响应。

在大多数情况下，除 [完成安装操作](finish-install-actions--windows-vista-and-later-.md)期间，共同安装程序不应与用户交互。 完成-安装操作在交互式上下文中运行。

**注意**   共同安装程序不应使用 ERROR_REQUIRES_INTERACTIVE_WINDOWSTATION 来使 DIF 代码失败，因为这会导致设备安装失败。 如果设备安装需要用户交互，则共同安装程序应支持完成安装操作。

 

## <a name="saving-device-installation-state"></a>正在保存设备安装状态


请勿将设备安装状态保存在 *共同安装程序* 动态链接库中 (DLL) 。 由于 Windows 通常在安装程序处理了一个 DIF 代码之后卸载 DLL，因此，在该 DLL 中保存的任何状态信息都不会保留。

为了安全地保留设备安装程序状态，类安装程序或共同安装程序应将状态信息保存为注册表中设备 *驱动程序密钥* 内的属性。 为此，请按照下列步骤进行操作：

1.  若要检索 *设备实例*的驱动程序密钥的注册表句柄，请使用 [**SetupDiOpenDevRegKey**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey) ，并将 *KeyType* 参数设置为 DIREG_DRV。

2.  使用 [**SetupDiGetDevicePropertyKeys**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys) (检索设备实例) 或 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) (的所有属性键以检索指定的设备实例属性项) 。

3.  使用 [**SetupDiSetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw) 保存设备实例属性项。

## <a name="loading-executable-or-dll-files"></a>加载可执行文件或 DLL 文件


如果你的 *共同安装程序* 尝试在 Windows 64 位平台上加载未签名的可执行文件或 DLL，则操作系统会阻止在此安全环境中加载它。

为了安全地通过类安装程序或共同安装程序加载可执行文件或 DLL，强烈建议将可执行文件或 DLL 包含在数字签名的 [驱动程序包](driver-packages.md)中。 有关如何对驱动程序包进行签名的详细信息，请参阅 [驱动程序签名](driver-signing.md)。

**注意**   类安装程序和共同安装程序不得通过显式函数调用（如**LoadLibrary**）或通过创建链接依赖项来加载 DLL 模块。

 

## <a name="starting-other-processes-or-services"></a>启动其他进程或服务


在设备安装过程中，Windows 无法跟踪其他进程，也无法确定其执行时间或完成时间。 例如，当进程执行关键操作时，Windows 可以启动或停止设备或启动系统重新启动。

在大多数情况下， *共同安装程序* 不应启动其他进程或服务。 但是，安装程序可以通过从通过[完成-安装操作](finish-install-actions--windows-vista-and-later-.md)显示的函数或对话框调用[CreateProcess](https://go.microsoft.com/fwlink/p/?linkid=194524)来安全地启动其他进程。 安装程序不得允许用户在对话框或过程中继续操作，直到创建的进程退出。

 

