---
title: 在 INF 文件中指定 WDF 指令
description: 在 INF 文件中指定 WDF 指令
ms.assetid: aefc678e-dc81-47dc-a84b-f1a79c16cad9
keywords:
- WDF 指令 WDK UMDF
- DDInstall 部分 WDK UMDF
- UmdfService INF 指令 WDK UMDF
- UmdfServiceOrder INF 指令 WDK UMDF
- UmdfImpersonationLevel INF 指令 WDK UMDF
- UmdfMethodNeitherAction INF 指令 WDK UMDF
- UmdfKernelModeClientPolicy INF 指令 WDK UMDF
- UmdfLibraryVersion INF 指令 WDK UMDF
- ServiceBinary INF 指令 WDK UMDF
- DriverCLSID INF 指令 WDK UMDF
- 指令 WDK UMDF
- 特定于 UMDF 的指令 WDK
- 服务的 UMDF 安装部分 WDK
- INF 文件 WDK UMDF，指令
- UmdfDispatcher INF 指令 WDK UMDF，语法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 265a68ae5e2139051e497fbd32321215bac2a70c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325127"
---
# <a name="specifying-wdf-directives-in-inf-files"></a>在 INF 文件中指定 WDF 指令


本主题适用于这两种用户模式驱动程序框架 (UMDF) 版本 1 和 2。

安装了 UMDF 驱动程序的 INF 文件必须包含 Microsoft Windows 驱动程序框架 (WDF) 的特定*DDInstall*部分。 INF 文件可以包含多个 WDF 特有*DDInstall*部分如果 INF 文件将安装多个 WDF 驱动程序。 每个 WDF 特有*DDInstall*部分：

-   对应于[ **DDInstall** ](https://msdn.microsoft.com/library/windows/hardware/ff547344)并[ **DDInstall.Services** ](https://msdn.microsoft.com/library/windows/hardware/ff547349)与特定的 WDF 驱动程序相关联的部分。

-   由所有加载 WDF 共同安装程序，运行按任意顺序进行处理。

-   包含用于设备的 WDF 安装指令。 特定于 UMDF 的指令以 UMDF 前缀开头，并特定于 KMDF 的指令以 KMDF 前缀开头。

下面的代码示例显示特定于 UMDF 的指令中 WDF 特定*DDInstall*部分。

```cpp
[Skeleton_Install.Wdf]
UmdfService=UMDFSkeleton,UMDFSkeleton_Install
UmdfServiceOrder=UMDFSkeleton
```

在特定于 WDF 的每个特定于 UMDF 的指令*DDInstall*部分以下列表中所述：

<a href="" id="umdfservice----servicename----sectionname-"></a>**UmdfService** = &lt;*serviceName*&gt;, &lt;*sectionName*&gt;  
将使用 UMDF 驱动程序相关联*UMDF 服务安装*节，其中包含安装 UMDF 驱动程序所需的信息。 *ServiceName*参数指定 UMDF 驱动程序，并限制为最多 31 个字符的长度。 *SectionName*参数引用*UMDF 服务安装*部分。 有效的 INF 文件通常需要至少**UmdfService**指令。 但是，如果 UMDF 驱动程序是操作系统的一部分**UmdfService** UMDF 驱动程序的指令则不需要。 因此，有效的 INF 文件可能不具有任何**UmdfService**指令，尽管大多数 INF 文件有一个**UmdfService**指令的每个 UMDF 驱动程序。

<a href="" id="umdfhostprocesssharing-------------processsharingdisabled---processsharingenabled-"></a>**UmdfHostProcessSharing** = &lt;**ProcessSharingDisabled** | **ProcessSharingEnabled**&gt;  
确定是否将设备堆栈放入共享的进程池 (**ProcessSharingEnabled**) 或其自己单独的进程 (**ProcessSharingDisabled**)。 默认值是**ProcessSharingEnabled**。 此指令是特定于设备的而不是特定于驱动程序。

有关设备池的详细信息，请参阅[UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)。

UMDF 版本 1.11 及更高版本支持**UmdfHostProcessSharing**指令。

<a href="" id="umdfdirecthardwareaccess----allowdirecthardwareaccess---rejectdirecthardwareaccess---"></a>**UmdfDirectHardwareAccess** = &lt;**AllowDirectHardwareAccess** | **RejectDirectHardwareAccess**&gt;   
指示框架是否应允许使用的任何硬件直接访问功能，如访问设备注册的驱动程序和端口，扫描硬件资源分配给设备，处理硬件中断，或获取连接资源。

如果**UmdfDirectHardwareAccess**设置为**AllowDirectHardwareAccess**，该框架允许使用 UMDF 接口执行直接访问硬件的驱动程序。

必须指定**AllowDirectHardwareAccess**如果 UMDF 驱动程序访问硬件资源，例如寄存器或端口、 中断[通用 I/O](https://msdn.microsoft.com/library/windows/hardware/hh439512) (GPIO) 的 pin 或此类串行总线连接I2C、 SPI，和串行端口。 您的驱动程序收到的所有这些资源通过*ResourcesRaw*并*ResourcesTranslated*的参数及其[ *EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数。

**请注意**  从 UMDF 2.15 版本开始，UMDF 驱动程序不需要指定**AllowDirectHardwareAccess**为了接收硬件资源列出了在其[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调例程。 如果未指定它，驱动程序没有要有一个例外使用这些资源的访问权限：

如果该设备分配一个或多个连接资源 (**CmResourceTypeConnection**) 和一个或多个中断资源 (**CmResourceTypeInterrupt**)，该驱动程序可以调用[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)从其[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调例程 (但不能从[ *EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693))。

 

有关将 UMDF 驱动程序连接到特定类型的资源的信息，请参阅：

-   [连接到 GPIO I/O 插针的 UMDF 驱动程序](https://msdn.microsoft.com/library/windows/hardware/hh698244)
-   [用户模式下存储外围设备驱动程序的硬件资源](https://msdn.microsoft.com/library/windows/hardware/hh450837)
-   [连接存储的外围设备的连接 Id](https://msdn.microsoft.com/library/windows/hardware/hh698216)
-   [连接到串行端口的外设的 UMDF 驱动程序](https://msdn.microsoft.com/library/windows/hardware/hh406559)

如果**UmdfDirectHardwareAccess**设置为**RejectDirectHardwareAccess**，框架不允许驱动程序，以使用任何硬件直接访问功能。 默认值是**RejectDirectHardwareAccess**。

有关如何 UMDF 驱动程序访问硬件资源的信息，请参阅[查找和映射硬件资源](finding-and-mapping-hardware-resources.md)。

UMDF 版本 1.11 及更高版本支持**UmdfDirectHardwareAccess**指令。

<a href="" id="umdfhostpriority----priorityhigh-"></a>**UmdfHostPriority** = &lt;**PriorityHigh**&gt;  
在 UMDF 版本 2.15 UMDF HID 自客户端驱动程序可以设置**UmdfHostPriority**到**PriorityHigh**提高其线程优先级。 此指令仅应该用于对用户响应时间不敏感的触摸或输入驱动程序。 当驱动程序指定了**PriorityHigh**，系统将其放入单独的设备池以及类似的优先级的其他驱动程序。 由于其他设备池使用更多的内存，因此应谨慎使用此设置。 有关设备池的详细信息，请参阅[UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)。

<a href="" id="umdfregisteraccessmode----registeraccessusingsystemcall---registeraccessusingusermodemapping--"></a>**UmdfRegisterAccessMode** = &lt;**RegisterAccessUsingSystemCall** | **RegisterAccessUsingUserModeMapping**&gt;   
指示框架是否应将映射到用户模式地址寄存器空间 （以使系统调用未参与访问寄存器），或使用系统调用来访问寄存器。

如果**UmdfRegisterAccessMode**设置为**RegisterAccessUsingSystemCall**，框架将使用系统调用访问寄存器。

如果**UmdfRegisterAccessMode**设置为**RegisterAccessUsingUserModeMapping**，框架将映射到用户模式地址空间的寄存器，以便访问寄存器不需要的系统调用。 默认值是**RegisterAccessUsingSystemCall**。

UMDF 版本 1.11 及更高版本支持**UmdfRegisterAccessMode**指令。

<a href="" id="--------umdfserviceorder----servicename1------servicename2------"></a> **UmdfServiceOrder** = &lt;*serviceName1*&gt; \[, &lt;*serviceName2*&gt; ...\]  
辅助安装程序将 UMDF 驱动程序安装在设备堆栈上按顺序列出。 即使辅助安装程序安装在设备堆栈上只有一个 UMDF 驱动程序，该 INF 文件必须包含此指令。 *ServiceNameXx*参数对应于*serviceName*每个参数**UmdfService**指令。 UMDF 驱动程序添加到设备堆栈中所列的顺序，因为第一个参数指定最低 UMDF 驱动程序设备堆栈中。

若要确保 UMDF 共同安装程序安装设备，只有一个**UmdfServiceOrder**指令必须存在于任何给定的 WDF 特定*DDInstall*部分。 即**UmdfServiceOrder**指令不能通过使用导入**Include**并**需要**指令。

<a href="" id="umdfimpersonationlevel----level-"></a>**UmdfImpersonationLevel** = &lt;*level*&gt;  
有关 UMDF 驱动程序可以具有的最大模拟级别通知框架。 一个**UmdfImpersonationLevel**指令是可选的; 如果未指定模拟级别，则默认值是**标识**。 当应用程序打开文件句柄时，该应用程序可以授予给驱动程序更高的模拟级别。 但是，该驱动程序不能调用[ **IWDFIoRequest::Impersonate** ](https://msdn.microsoft.com/library/windows/hardware/ff559136)方法来请求模拟级别大于级别的**UmdfImpersonationLevel**指定。 此指令的可能值是：

-   **匿名**

-   **Identification**

-   **模拟**

-   **委派**

这些值对应于中指定的值[**安全\_模拟\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff560499)枚举。

<a href="" id="umdfmethodneitheraction------------copy---reject-"></a>**UmdfMethodNeitherAction** = &lt;**Copy** | **Reject**&gt;  
指示是否将接受该框架 (**副本**) 或拒绝 (**拒绝**) 设备的 I/O 请求时，如果请求对象包含指定的 I/O 控制代码[方法\_NEITHER](https://msdn.microsoft.com/library/windows/hardware/ff540663)缓冲访问方法。 一个**UmdfMethodNeitherAction**指令是可选的。 如果不指定指令，默认值是**拒绝**。

有关支持该方法的详细信息\_请参阅基于 UMDF 驱动程序中的访问方法都不缓冲区[使用既不缓冲 I/O，也不在 UMDF 驱动程序的直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff554413#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)。

<a href="" id="umdfdispatcher----filehandle---winusb---nativeusb-"></a>**UmdfDispatcher** = &lt;**FileHandle** | **WinUsb** | **NativeUSB**&gt;  
通知框架将 I/O 发送 I/O 经历设备堆栈的用户模式部分后的位置。 默认情况下，I/O 发送到该发送程序 (WUDFRd.sys)。 通过设置**UmdfDispatcher**到**WinUsb**，驱动程序将指示 UMDF 将 I/O 发送到 WinUsb 体系结构。 启动在 UMDF 2.15、 指定**NativeUSB**会导致该发送程序来处理 USB I/O。

-   如果堆栈中的任何驱动程序使用基于文件句柄的目标，此指令设置为**FileHandle**。
-   如果该驱动程序使用 UMDF 2.15 或更高版本，并使用 USB I/O 目标，此指令设置为**NativeUSB**。
-   如果该驱动程序之前 UMDF 2.15 且使用 USB I/O 目标，此指令设置为**WinUsb**。

一个**UmdfDispatcher**指令是可选的。

下面的代码示例演示**UmdfDispatcher** WDF 特定指令**DDInstall**部分。

```cpp
[Xxx_Install.Wdf]
UmdfDispatcher=NativeUSB
```

<a href="" id="umdfkernelmodeclientpolicy------------allowkernelmodeclients---rejectkernelmodeclients-"></a>**UmdfKernelModeClientPolicy** = &lt;**AllowKernelModeClients** | **RejectKernelModeClients**&gt;  
指示框架是否应允许驱动程序从内核模式驱动程序接收的 I/O 请求。

如果**UmdfKernelModeClientPolicy**设置为**AllowKernelModeClients**，框架允许要高于用户模式驱动程序，加载的内核模式驱动程序，它提供从内核模式驱动程序的 I/O 请求对用户模式驱动程序。

如果**UmdfKernelModeClientPolicy**设置为**RejectKernelModeClients**，框架不允许使用内核模式驱动程序以加载用户模式驱动程序，且它不会从任何提供 I/O 请求对用户模式驱动程序的内核模式驱动程序。 如果驱动程序的 INF 文件不包含此指令，则默认值是**RejectKernelModeClients**。 有关详细信息，请参阅[支持内核模式下客户端](https://msdn.microsoft.com/library/windows/hardware/ff561214)。

UMDF 版本 1.9 及更高版本支持**UmdfKernelModeClientPolicy**指令。 若要允许要高于早期 UMDF 版本中的用户模式驱动程序加载的内核模式驱动程序，请参阅[内核模式下客户端支持在早期版本中 UMDF](https://msdn.microsoft.com/library/windows/hardware/ff561214#kernel-mode-client-support-in-earlier-umdf-versions)。

<a href="" id="umdffileobjectpolicy----rejectnullandunknownfileobjects---allownullandunknownfileobjects--"></a>**UmdfFileObjectPolicy** = &lt;**RejectNullAndUnknownFileObjects** | **AllowNullAndUnknownFileObjects**&gt;   
指示框架是否应允许处理的 I/O 请求 ([IWDFIoRequest](https://msdn.microsoft.com/library/windows/hardware/ff558985))，或者不与关联的文件对象 ([IWDFFile](https://msdn.microsoft.com/library/windows/hardware/ff558912)) 或与 (a 未知的文件对象相关联文件对象中为其驱动程序具有以前未见过创建请求）。

如果**UmdfFileObjectPolicy**设置为**RejectNullAndUnknownFileObjects**，框架不允许与 NULL 或未知文件对象相关联的请求的处理。

如果**UmdfFileObjectPolicy**设置为**AllowNullAndUnknownFileObjects**，该框架允许与 NULL 或未知文件对象相关联的请求的处理。

默认值是**RejectNullAndUnknownFileObjects**。

UMDF 版本 1.11 及更高版本支持**UmdfFileObjectPolicy**指令。

<a href="" id="umdffscontextusepolicy----canusefscontext---canusefscontext2----cannotusefscontexts-"></a>**UmdfFsContextUsePolicy** = &lt;**CanUseFsContext** | **CanUseFsContext2** | **CannotUseFsContexts**&gt;  
指示框架是否可以将内部信息存储在特定上下文 WDM 文件对象的成员。 如果同一堆栈中的内核模式驱动程序使用特定的文件对象的成员，可以使用此指令以请求该框架不使用相同的位置。

如果**UmdfFsContextUsePolicy**设置为**CanUseFsContext**，框架将信息存储**FsContext** WDM 文件对象的成员。

如果**UmdfFsContextUsePolicy**设置为**CanUseFsContext2**，框架将信息存储**FsContext2** WDM 文件对象的成员。

如果**UmdfFsContextUsePolicy**设置为**CannotUseFsContexts**，该框架不使用任何一个**FsContext**或者**FsContext2**。

默认值是**CanUseFsContext**。

UMDF 版本 1.11 及更高版本支持**UmdfFsContextUsePolicy**指令。




下面的代码示例显示了中的所需的指令*UMDF 服务安装*部分。

```cpp
[UMDFSkeleton_Install]
UmdfLibraryVersion=1.0.0
ServiceBinary=%12%\UMDF\UMDFSkeleton.dll
DriverCLSID={d4112073-d09b-458f-a5aa-35ef21eef5de}
```

中的每个指令*UMDF 服务安装*部分以下列表中所述：

<a href="" id="umdflibraryversion------------version-"></a>**UmdfLibraryVersion** = &lt;*version*&gt;  
辅助安装程序会告知 UMDF 驱动程序将使用 framework 的版本号。 格式*版本*字符串&lt;*主要*&gt;。&lt;*次要*&gt;。&lt;*服务*&gt;。 当设备堆栈上的驱动程序使用多个版本的 framework 时，INF 文件将多个共同安装程序-一个用于每个框架版本--复制到硬盘驱动器上的同一位置。 但是，INF 文件将添加仅的最高版本共同安装程序**CoInstallers32**注册表值。 有关复制共同安装程序的详细信息，请参阅[使用 UMDF 共同安装程序](using-the-umdf-co-installer.md)。

辅助安装程序验证的版本字符串，并使用它来查找 UMDF 驱动程序的特定于版本的共同安装程序。 辅助安装程序然后提取特定于版本的共同安装程序的框架。

<a href="" id="servicebinary----binarypath-"></a>**ServiceBinary** = &lt;*binarypath*&gt;  
有关在何处放置 UMDF 驱动程序在硬盘驱动器上二进制通知 UMDF。

应复制到，UMDF 驱动程序，并将其从，运行\\Windows\\System32\\驱动程序\\UMDF 目录。

<a href="" id="driverclsid-----clsid--"></a>**DriverCLSID** = &lt;{*CLSID*}&gt;  
**请注意**  UMDF 版本 1.11 中及更早版本，此指令很。

UMDF 告知 UMDF 驱动程序的类标识符 (CLSID)。 UMDF 主机时 UMDF 加载 UMDF 驱动程序，使用 UMDF 驱动程序的 CLSID 来创建实例的 UMDF 驱动程序的[IDriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff554885)接口。

<a href="" id=" umdfextensions-----cxservicename--"></a>**UmdfExtensions** = &lt;cxServiceName&gt;用于通信的驱动程序与 Microsoft 提供的类扩展驱动程序。  CxServiceName 参数对应于二进制的类扩展驱动程序与关联的服务。

类扩展驱动程序的服务名称找不到作为下以下注册表项的子项：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\WUDF\Services**

在 Windows 8.1 及更早版本，若要避免需要重新启动更新 UMDF 驱动程序时，指定**COPYFLG\_IN\_使用\_重命名**标志中[ **CopyFiles指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346)在驱动程序的 INF 文件中，在此示例中所示：

```cpp
[VirtualSerial_Install.NT]
CopyFiles=UMDriverCopy
 
[UMDriverCopy]
Virtualserial.dll,,,0x00004000  ; COPYFLG_IN_USE_RENAME
```

 

 





