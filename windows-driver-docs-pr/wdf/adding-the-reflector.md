---
title: INF 文件中指定该发送程序
description: INF 文件中指定该发送程序
ms.assetid: 3676c99d-4e13-4385-910a-251232b00d4c
keywords:
- 发送程序 WDK UMDF
- AddService
- INF 文件 WDK UMDF，发送程序
- 函数的 WDK UMDF 驱动程序
- 筛选器驱动程序 WDK UMDF
- 正在加载发送程序 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bec546532b0d656dc3a493e30ff1a7d7dd34c2b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350721"
---
# <a name="specifying-the-reflector-in-an-inf-file"></a>INF 文件中指定该发送程序


若要将该发送程序 (WUDFRd.sys) 添加到内核模式设备堆栈，UMDF 驱动程序的 INF 文件必须包括[ **AddService 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546326)中[ **INF DDInstall.Services部分**](https://msdn.microsoft.com/library/windows/hardware/ff547349)。 该发送程序可以是上部的筛选器、 较低的筛选器或该设备，具体取决于用户模式堆栈配置的服务。

下面的代码示例说明了如何 UMDF 功能驱动程序的 INF 文件可能会添加该发送程序。

```cpp
[Skeleton_Install.Services]
AddService=WUDFRd,0x000001fa,WUDFRD_ServiceInstall
```

在此示例中，该驱动程序指定 0x2 (SPSVCINST\_ASSOCSERVICE) 标志 (或运算到*标志*上述参数) 以将该发送程序指定为内核模式设备堆栈中的函数驱动程序。

**AddService**指令还会设置 0x000001f8 标志，以防止覆盖任何预先存在的服务配置。 有关这些标志的详细信息，请参阅*标志*的参数[ **AddService 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546326)。

下面的代码示例摘自 WUDFVhidmini 示例，演示**AddService** UMDF 筛选器驱动程序的指令。

```cpp
[hidumdf.win8.NT.Services]
AddService=WUDFRd,0x000001f8,WUDFRD_ServiceInstall  
AddService=mshidumdf, 0x000001fa, mshidumdf.AddService

[WudfVhidmini_AddReg]
HKR,,"LowerFilters",0x00010008,"WUDFRd" ; FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
```

在这种情况下，mshidumdf 服务与设备堆栈 FDO、 反射器是一个较低的筛选器。

## <a name="providing-a-service-install-section"></a>提供一个服务安装部分


**AddService**指令引用服务的安装-部分类似于下面的代码示例。 **ServiceType**条目指定 1 或 0x00000001，指示 INF 安装的一个或多个设备的支持。 **StartType**条目指定何时启动驱动程序。 **ErrorControl**条目指定的驱动程序提供的错误控制级别。 **ServiceBinary**条目指定服务的二进制文件 （该发送程序） 的路径。

```cpp
[WUDFRD_ServiceInstall]
DisplayName = "Windows Driver Frameworks - User-mode Driver Framework Reflector"
ServiceType=1
StartType=3
ErrorControl=1
ServiceBinary=%12%\WUDFRd.sys
```

## <a name="specifying-a-unique-service-name"></a>指定唯一的服务名称


虽然不要求必须这样做，但只能在 Windows 8 和更高版本操作系统运行的 UMDF 驱动程序可以指定 WUDFRd （反射） 服务的唯一服务名称。

下面的示例演示如何指定唯一的服务名称而不是 WUDFRd。

```cpp
[Echo_Install.NT.Services]
AddService=WudfEchoDriver,0x00000002,WUDFEchoDriver_ServiceInstall

[WUDFEchoDriver_ServiceInstall]
DisplayName = %WudfEchoDriverDisplayName%
ServiceType = 1
StartType = 3
ErrorControl = 1
ServiceBinary = %12%\WUDFRd.sys
StartName = \Driver\WudfRd
```

在上述示例中，该驱动程序指定唯一值中的服务名称**AddService**指令。 （在这种情况下，它是 WudfEchoDriver，这是驱动程序的名称。）接下来，驱动程序指定一个唯一**DisplayName**服务的值。 最后，该驱动程序添加**StartName**条目并将其设置为\\驱动程序\\WudfRd。

UMDF 驱动程序不能指定唯一的服务名称为该发送程序上的操作系统早于 Windows 8。 如果您的驱动程序指定唯一的服务名称，但还必须处理的操作系统早于 Windows 8，如下面的示例中所示使用在 INF 文件中，操作系统特定部分。

```cpp
[Manufacturer]
%MSFT% = Microsoft,NTx86.6.0,NTx86.6.2
[Microsoft.NTx86.6.0]
%Sensors.DeviceDesc% = Sensors_Install_VistaWin7,HID_DEVICE_UP:0020_U:0001
[Microsoft.NTx86.6.2]
%Sensors.DeviceDesc% = Sensors_Install_Win8,HID_DEVICE_UP:0020_U:0001
[Sensors_Install_VistaWin7]
--- Install the device this way on Vista/Win7 ---
[Sensors_Install_Win8]
--- Install the device in a different way on Win8 ---
```

如果未添加该发送程序，永远不加载 UMDF。 设备可能会启动，但主机进程不存在并且设备将无法正常运行。

 

 





