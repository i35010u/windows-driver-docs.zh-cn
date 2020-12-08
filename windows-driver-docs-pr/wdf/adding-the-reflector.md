---
title: 在 INF 文件中指定反射器
description: 在 INF 文件中指定反射器
keywords:
- 发送程序 WDK UMDF
- AddService
- INF 文件 WDK UMDF，发送程序
- 函数驱动程序 WDK UMDF
- 筛选器驱动程序 WDK UMDF
- 加载发送程序 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a0ecf2acef7dd5bbb95e10011b115b363bf3884
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815793"
---
# <a name="specifying-the-reflector-in-an-inf-file"></a>在 INF 文件中指定反射器


要向内核模式设备堆栈添加反射器 ( # A0) ，UMDF 驱动程序的 INF 文件必须在 [**Inf DDInstall 部分**](../install/inf-ddinstall-services-section.md)中包含 [**AddService 指令**](../install/inf-addservice-directive.md)。 反射器可以是上限、下限或设备的服务，具体取决于用户模式堆栈的配置。

下面的代码示例演示如何使用 UMDF 函数驱动程序的 INF 文件来添加反射器。

```cpp
[Skeleton_Install.Services]
AddService=WUDFRd,0x000001fa,WUDFRD_ServiceInstall
```

在此示例中，驱动程序将 0x2 (SPSVCINST \_ ASSOCSERVICE) 标志 (运算指定为上述 *flags* 参数，) 将该反射器指定为内核模式设备堆栈中的函数驱动程序。

**AddService** 指令还会设置0x000001f8 标志，以防止覆盖服务的任何预先存在的配置。 有关这些标志的详细信息，请参阅 [**AddService 指令**](../install/inf-addservice-directive.md)的 *flags* 参数。

下面的代码示例摘自 WUDFVhidmini 示例，它显示了用于 UMDF 筛选器驱动程序的 **AddService** 指令。

```cpp
[hidumdf.win8.NT.Services]
AddService=WUDFRd,0x000001f8,WUDFRD_ServiceInstall  
AddService=mshidumdf, 0x000001fa, mshidumdf.AddService

[WudfVhidmini_AddReg]
HKR,,"LowerFilters",0x00010008,"WUDFRd" ; FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
```

在这种情况下，mshidumdf 服务与设备堆栈的 FDO 相关联，而反射器是较低的筛选器。

## <a name="providing-a-service-install-section"></a>提供服务安装部分


**AddService** 指令引用类似于下面的代码示例的服务安装部分。 **ServiceType** 条目指定1或0x00000001，这表示 INF 安装了对一个或多个设备的支持。 **StartType** 条目指定启动驱动程序的时间。 **ErrorControl** 项指定驱动程序提供的错误控制级别。 **ServiceBinary** 项指定服务的反射器) 的二进制 (路径。

```cpp
[WUDFRD_ServiceInstall]
DisplayName = "Windows Driver Frameworks - User-mode Driver Framework Reflector"
ServiceType=1
StartType=3
ErrorControl=1
ServiceBinary=%12%\WUDFRd.sys
```

## <a name="specifying-a-unique-service-name"></a>指定唯一的服务名称


虽然这不是必需的，但仅在 Windows 8 及更高版本的操作系统上运行的 UMDF 驱动程序可以为 WUDFRd (反射器) 服务指定唯一的服务名称。

下面的示例演示如何指定唯一的服务名称，而不是 WUDFRd。

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

在上面的示例中，驱动程序在 **AddService** 指令中指定服务名称的唯一值。  (在这种情况下，它是 WudfEchoDriver，它是驱动程序的名称。 ) 接下来，驱动程序为服务 **指定唯一的** 显示名称值。 最后，驱动程序添加 **StartName** 项并将其设置为 \\ 驱动程序 \\ WudfRd。

UMDF 驱动程序无法为 Windows 8 之前的操作系统上的反射器指定唯一的服务名称。 如果驱动程序指定唯一的服务名称，但也必须在早于 Windows 8 的操作系统上运行，请在 INF 文件中使用特定于操作系统的部分，如以下示例中所示。

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

如果未添加反射器，则不会加载 UMDF。 设备可能会启动，但不存在主机进程，并且设备将无法正常运行。

 

