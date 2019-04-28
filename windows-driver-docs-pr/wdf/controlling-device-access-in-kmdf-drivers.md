---
title: 在 KMDF 驱动程序中控制设备访问权限
description: 在 KMDF 驱动程序中控制设备访问权限
ms.assetid: 62bbc69f-0754-4d37-a476-dd2ac3d70de6
keywords:
- 设备的访问控制 WDK KMDF
- WDK 设备对象的名称
- 设备对象 WDK KMDF
- framework 对象 WDK KMDF，设备的访问控制
- 安全描述符 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33a33723f3477377f2dec3da86bc56b7eeb44df4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340867"
---
# <a name="controlling-device-access-in-kmdf-drivers"></a>在 KMDF 驱动程序中控制设备访问权限


驱动程序必须帮助防止用户不恰当地访问计算机的设备和文件。 若要防止未经授权的访问设备和文件，必须：

-   名称仅在必要时的设备对象。

-   提供设备对象和接口的安全描述符。

### <a href="" id="naming-device-objects-only-when-necessary"></a> 仅在必要时命名的设备对象

大多数 Windows 驱动程序模型 (WDM) 驱动程序，如基于框架的驱动程序通常名称用其设备对象。 应用程序可以通过指定设备对象名称，因此每个附加的设备对象名称表示应用程序可用于访问设备的其他路径访问设备。

若要防止未经授权的访问设备，每个驱动程序可以名称的设备对象时指定的安全描述符。 但是的文件的名称的操作系统提供了到驱动程序 (，请参阅[ **WdfFileObjectGetFileName**](https://msdn.microsoft.com/library/windows/hardware/ff547310)) 不包括应用程序使用的设备对象名称。 因此，如果您的驱动程序堆栈中的多个驱动程序提供其设备对象的名称，您的驱动程序无法确定应用程序用来打开设备的对象名称。 因此，应用程序可能使用限制性较弱的安全描述符比您的驱动程序所需打开设备。

物理设备对象 (PDOs) 必须具有名称。 通常情况下，基于框架的总线驱动程序不要指定 PDO 的名称，因为默认情况下 framework 指示操作系统生成的名称。

另一方面，基于框架的驱动程序可以将一个设备名称到设备对象通过调用[ **WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)。 驱动程序应命名功能的设备对象 (FDO)、 筛选设备对象 （筛选器执行操作） 或 PDO，仅当该驱动程序必须支持的较旧的应用程序需要特定的设备名称，或如果驱动程序属于较旧的驱动程序堆栈的体系结构要求对象名称。

而不是命名 FDOs 和筛选器 DOs，WDM 驱动程序和基于框架的驱动程序应提供应用程序可以访问的设备接口。 从设备的 PDO 和驱动程序包的 INF 文件指定的注册表项，操作系统将获取设备接口的安全描述符。 如果在 raw 模式，而无需功能驱动程序的驱动程序的设备操作，总线驱动程序可以对 PDO 提供设备接口。

某些驱动程序必须调用[ **WdfDeviceCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff545939)创建符号链接为其设备的名称。 例如，可以创建一个驱动程序[MS-DOS 设备名称](https://msdn.microsoft.com/library/windows/hardware/ff548088)如果应用程序会看到设备的 MS-DOS 名称。 如果您的驱动程序创建的未命名的 FDO 或筛选器的符号链接名称执行操作，框架将 PDO 的名称与相关联的符号链接名称。 （控制的设备不与相关联的 PDO，因此您的驱动程序不能创建未命名的控制设备的符号链接名称。）

### <a href="" id="providing-security-descriptors-for-device-objects-and-interfaces"></a> 提供有关设备对象和接口的安全描述符

每个指定的设备对象必须具有安全描述符。 操作系统使用设备对象的安全描述符来确定用户有权访问设备和其设备接口的类型。 安全描述符可以分配给由设备对象：

-   操作系统，提供设备对象的默认安全描述符 (请参阅[控制的设备访问](https://msdn.microsoft.com/library/windows/hardware/ff542063))。

-   框架，它提供了默认安全描述符 (通过使用 SDDL\_DEVOBJ\_SYS\_所有\_ADM\_所有值) 如果您的驱动程序调用[ **WdfDeviceInitAssignName** ](https://msdn.microsoft.com/library/windows/hardware/ff546029)若要为设备对象分配一个名称 (请参阅[设备对象的 SDDL](https://msdn.microsoft.com/library/windows/hardware/ff563667))。

-   您的驱动程序，可以通过调用来替代框架的默认安全描述符[ **WdfDeviceInitAssignSDDLString**](https://msdn.microsoft.com/library/windows/hardware/ff546035)。

默认情况下，操作系统还使用设备 PDO 安全描述符以确定驱动程序提供的设备接口的访问权限。

驱动程序包可以提供一个指定与设备的安全描述符的 INF 文件[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)内[ **INF DDInstall.HW 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547330).

有关在 INF 文件中指定安全描述符的详细信息，请参阅[创建安全的设备安装](https://msdn.microsoft.com/library/windows/hardware/ff540212)。

如果您的驱动程序创建 PDOs 的设备的操作在 raw 模式，该驱动程序必须指定[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)当调用[ **WdfPdoInitAssignRawDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548802)。 此外，如果您的驱动程序创建控制的设备，它可以调用[ **WdfDeviceInitSetDeviceClass** ](https://msdn.microsoft.com/library/windows/hardware/ff546084)指定设备安装程序类。 在这种情况下，系统管理员可以使用指定的安装程序类的注册表项来存储设备的安全描述符。

有关操作系统如何确定要使用设备的安全描述符信息，请参阅[控制的设备访问](https://msdn.microsoft.com/library/windows/hardware/ff542063)。

当框架将创建一个设备对象时，它始终会设置文件\_设备\_SECURE\_打开标志，以便操作系统将允许应用程序访问的任何名称前检查设备的安全描述符在设备的命名空间。 有关文件的详细信息\_设备\_SECURE\_打开标志和设备的命名空间，请参阅[控制设备 Namespace 访问](https://msdn.microsoft.com/library/windows/hardware/ff542068)。

 

 





