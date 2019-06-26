---
title: INF AddService 指令
description: AddService 指令使用 INF DDInstall.Services 部分或 INF DefaultInstall.Services 部分内。
ms.assetid: 3314da8b-3fde-462a-a64d-a0514710663a
keywords:
- INF AddService 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF AddService Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be29020ed3df4a8661278bf9cbf4c23c2a5587ea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385920"
---
# <a name="inf-addservice-directive"></a>INF AddService 指令


**请注意**  安装不需要任何驱动程序，如调制解调器或显示监视器的设备的 INF 文件中不使用此指令。

 

**AddService**中使用指令[ **INF *DDInstall*。服务部分**](inf-ddinstall-services-section.md)或[ **INF DefaultInstall.Services 部分**](inf-defaultinstall-services-section.md)。 它指定与驱动程序，例如和服务已被加载和其他基础旧驱动程序或服务上的任何依赖项关联的服务的特征。 （可选） 此指令还会设置设备的事件日志记录服务。

```ini
[DDInstall.Services] 
 
AddService=ServiceName,[flags],service-install-section
                     [,event-log-install-section[,[EventLogType][,EventName]]]
...
```

## <a name="entries"></a>条目


<a href="" id="servicename"></a>*ServiceName*  
指定要安装的服务的名称。 对于设备，此值通常是其驱动程序，例如"sermouse，"有通用名称或一些此类名称。 此名称必须不会本地化。 它必须是而不考虑系统的本地语言相同。

<a href="" id="flags"></a>*flags*  
指定一个或多个 （或运算） 的以下系统定义标志，在中定义*Setupapi.h*表示为十六进制值：

<a href="" id="0x00000001--spsvcinst-tagtofront-"></a>**0x00000001** (SPSVCINST_TAGTOFRONT)  
将指定的服务标记移到其组顺序列表中，从而确保它加载的第一次该组内 （除非此 INF 规范与以后安装的设备将取代它） 开头。 使用 WDM 驱动程序安装以独占方式即插即用设备和设备的 INF 文件不应设置此标志。

<a href="" id="0x00000002--spsvcinst-assocservice-"></a>**0x00000002** (SPSVCINST_ASSOCSERVICE)  
将指定的服务分配为即插即用功能驱动程序 （或旧版的驱动程序），此 INF 文件正在安装设备。

若要指示服务是一种设备功能驱动程序，该服务应指定**SPSVCINST_ASSOCSERVICE**中的标志**AddService**指令。  筛选器驱动程序或其他驱动程序组件等服务，不应使用此标志。

每个设备驱动程序 INF 应具有一个关联的服务。  INF 不需要关联的服务，如果它是扩展或使用 Include/需要指令以从另一个 INF 继承关联的服务。  对于不需要功能驱动程序的设备，可以按如下所示指定 NULL 驱动程序：

```
AddService = ,2.
```

<a href="" id="0x00000008--spsvcinst-noclobber-displayname-"></a>**0x00000008** (SPSVCINST_NOCLOBBER_DISPLAYNAME)  
如果在系统中已存在此服务不会覆盖给定的服务的 （可选） 的友好名称。

<a href="" id="0x00000010--spsvcinst-noclobber-starttype-"></a>**0x00000010** (SPSVCINST_NOCLOBBER_STARTTYPE)  
如果此已命名服务在系统中存在，则不会覆盖给定的服务的启动类型。

<a href="" id="0x00000020--spsvcinst-noclobber-errorcontrol-"></a>**0x00000020** (SPSVCINST_NOCLOBBER_ERRORCONTROL)  
如果此已命名服务在系统中存在，则不会覆盖给定的服务的错误控制值。

<a href="" id="0x00000040--spsvcinst-noclobber-loadordergroup-"></a>**0x00000040** (SPSVCINST_NOCLOBBER_LOADORDERGROUP)  
如果此已命名服务在系统中存在，则不会覆盖给定的服务的加载顺序组值。 使用 WDM 驱动程序安装以独占方式即插即用设备和设备的 INF 文件不应设置此标志。

<a href="" id="0x00000080--spsvcinst-noclobber-dependencies--"></a>**0x00000080** (SPSVCINST_NOCLOBBER_DEPENDENCIES)   
如果此已命名服务在系统中存在，则不会覆盖给定的服务的依赖项列表。 使用 WDM 驱动程序安装以独占方式即插即用设备和设备的 INF 文件不应设置此标志。

<a href="" id="0x00000100--spsvcinst-noclobber-description-"></a>**0x00000100** (SPSVCINST_NOCLOBBER_DESCRIPTION)  
如果在系统中已存在此服务不会覆盖给定的服务的说明 （可选）。

<a href="" id="0x00000400--spsvcinst-clobber-security---windows-xp-and-later-versions-of-windows--"></a>**0x00000400** (SPSVCINST_CLOBBER_SECURITY) （Windows XP 和更高版本的 Windows）   
如果在系统中已存在此服务，则覆盖该服务的安全设置。

<a href="" id="0x00000800--spsvcsinst-startservice---windows-vista-and-later-versions-of-windows--"></a>**0x00000800** (SPSVCSINST_STARTSERVICE) （Windows Vista 和更高版本的 Windows）   
安装了服务后，请启动该服务。 此标志不能用于启动实现插即用 (PnP) 功能驱动程序或设备的筛选器驱动程序的服务。 否则，此标志可以用于启动托管的服务控制管理器 (SCM) 的用户模式或内核模式服务。

<a href="" id="0x00001000--spsvcinst-noclobber-requiredprivileges---windows-7-and-later-versions-of-windows-"></a>**0x00001000** (SPSVCINST_NOCLOBBER_REQUIREDPRIVILEGES) （Windows 7 和更高版本的 Windows）  
如果在系统中已存在此服务不会覆盖给定服务的特权。

<a href="" id="service-install-section"></a>*service-install-section*  
引用了一个 INF 编写器定义的部分，其中包含用于安装此设备 （或设备） 的命名的服务的信息。 有关详细信息，请参阅以下**备注**部分。

<a href="" id="event-log-install-section"></a>*event-log-install-section*  
根据需要引用在其中设置为此设备 （或设备） 的事件日志记录服务 INF 编写器定义的部分。

<a href="" id="eventlogtype"></a>*EventLogType*  
（可选） 指定之一**系统**，**安全**，或**应用程序**。 如果省略，则此值默认为**系统**，这几乎始终是安装设备驱动程序的相应值。

例如，将指定 INF**安全**仅当要安装的驱动程序提供其自己的安全支持。

<a href="" id="eventname"></a>*EventName*  
（可选） 指定要使用的事件日志的名称。 如果省略，则此值默认为给定*ServiceName*。

<a name="remarks"></a>备注
-------

系统定义的和不区分大小写扩展可以插入到<em>DDInstall</em> **。服务**节，其中包含**AddService**指令跨操作系统系统和/或跨平台 INF 文件中指定特定于平台的或特定于操作系统的安装。

每个 INF 编写器创建的部分名称的 INF 文件中必须是唯一和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

**AddService**指令必须引用一个已命名*服务安装部分*INF 文件中的其他位置。 每个此类部分具有以下形式：

```ini
[service-install-section]
 
[DisplayName=name]
[Description=description-string]
ServiceType=type-code
StartType=start-code
ErrorControl=error-control-level
ServiceBinary=path-to-service
[StartName=driver-object-name]
[AddReg=add-registry-section[, add-registry-section] ...]
[DelReg=del-registry-section[, del-registry-section] ...]
[BitReg=bit-registry-section[,bit-registry-section] ...]
[LoadOrderGroup=load-order-group-name]
[Dependencies=depend-on-item-name[,depend-on-item-name]
[Security="security-descriptor-string"]...]
```

每个*服务安装部分*必须具有至少**ServiceType**， **StartType**， **ErrorControl**，和**ServiceBinary**条目如下所示。 但是，剩余的条目是可选的。

### <a name="service-install-section-entries-and-values"></a>服务安装节条目和值

<a href="" id="displayname-name"></a>**DisplayName**=*name*  
通常情况下，指定服务/驱动程序的友好名称，以便于本地化，表示为 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md) INF 文件部分。

<a href="" id="description-description-string"></a>**描述**=*描述字符串*  
（可选） 指定一个字符串，描述服务，通常表示为 %*strkey*中定义的 %令牌**字符串**INF 文件部分。

此字符串将提供用户与服务有关的详细信息**DisplayName**。 例如， **DisplayName**可能是诸如"DHCP 客户端"和描述可能类似于"管理注册和更新 IP 地址和 DNS 名称的网络配置"。

*描述字符串*应足够长，为具有描述性，而且非常不方便，并不太长。 如果*描述字符串*包含任何 %*strkey*%令牌，每个标记可以表示 511 个字符最大值。 字符串的总后任何字符串令牌替换，不应超过 1024年个字符。

<a href="" id="servicetype-type-code"></a>**ServiceType**=*type-code*  
内核模式设备驱动程序的类型代码必须设置为 0x00000001 (SERVICE_KERNEL_DRIVER)。

*类型代码*设备应设置为安装的 Microsoft Win32 服务**0x00000010** (SERVICE_WIN32_OWN_PROCESS) 或**0x00000020** (SERVICE_WIN32_SHARE_PROCESS)。 如果 Win32 服务可以与桌面进行交互，类型代码值应合并在一起**0x00000100** (SERVICE_INTERACTIVE_PROCESS)。

*类型代码*为最高级别网络驱动程序，例如重定向器或文件系统驱动程序，应设置为**0x00000002** (SERVICE_FILE_SYSTEM_DRIVER)。

在中定义的 SERVICE_xxxx 常量*wdm.h 中*并*Ntddk.h*。

<a href="" id="starttype-start-code"></a>**StartType**=*start-code*  
指定何时启动驱动程序作为一个可以用十进制表示以下数字值，或如以下列表中，以十六进制表示法中所示。

<a href="" id="0x0--service-boot-start-"></a>**0x0** (SERVICE_BOOT_START)  
指示由操作系统加载程序启动的驱动程序。

此值必须用于加载操作系统所需的设备驱动程序。

<a href="" id="0x1--service-system-start-"></a>**0x1** (SERVICE_SYSTEM_START)  
指示操作系统初始化过程中启动了驱动程序。

通过执行在初始化过程中的设备检测操作，但不是需要加载系统的即插即用驱动程序应使用此值。

例如，还可以检测旧设备的即插即用驱动程序应指定此值在其 INF 因此，其[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程称为查找旧的设备，即使该设备不能为枚举即插即用管理器。

<a href="" id="0x2--service-auto-start-"></a>**0x2** (SERVICE_AUTO_START)  
指示在系统启动期间由服务控制管理器启动的驱动程序。

此值应永远不会使用 INF 文件中为 WDM 或即插即用设备驱动程序。

<a href="" id="0x3--service-demand-start-"></a>**0x3** (SERVICE_DEMAND_START)  
指示按需、 通过枚举相应设备时的即插即用管理器或可能是由服务控制管理器响应非 PnP 设备显式用户要求启动的驱动程序。

此值应在所有 WDM 驱动程序的设备不需要加载系统的和未加载系统所需或不参与设备检测所有即插即用设备驱动程序的 INF 文件中使用。

<a href="" id="0x4--service-disabled-"></a><strong>0x4 (</strong>SERVICE_DISABLED)  
指示不能启动的驱动程序。

此值可以用于暂时禁用设备的驱动程序服务。 但是，如果其 INF 文件的服务安装部分中指定此值，则无法安装设备/驱动程序。

有关详细信息**StartType**，请参阅[指定驱动程序加载顺序](specifying-driver-load-order.md)。

<a href="" id="errorcontrol-error-control-level"></a>**ErrorControl**=*error-control-level*  
作为以下数字值，可以用十进制表示之一，或如图所示，在以下列表中，以十六进制表示法指定错误控制的级别。

<a href="" id="0x0--service-error-ignore-"></a>**0x0** (SERVICE_ERROR_IGNORE)  
如果该驱动程序无法加载或初始化，请继续执行系统启动时并不向用户显示一条警告。

<a href="" id="0x1--service-error-normal-"></a>**0x1** (SERVICE_ERROR_NORMAL)  
如果该驱动程序无法加载或初始化其设备，系统启动时应继续，但向用户显示一条警告。

<a href="" id="0x2--service-error-severe-"></a>**0x2** (SERVICE_ERROR_SEVERE)  
如果无法加载该驱动程序，系统启动时应切换到注册表**LastKnownGood**控件集和继续系统启动时，即使该驱动程序再次指示加载或设备/驱动程序初始化错误。

<a href="" id="0x3--service-error-critical-"></a>**0x3** (SERVICE_ERROR_CRITICAL)  
如果无法加载该驱动程序和系统启动时未使用的注册表**LastKnownGood**控件集，请切换到**LastKnownGood** ，然后重试。

如果使用时，启动仍然无法正常工作**LastKnownGood**，运行错误检查例程。 (*仅*设备/驱动程序所需系统引导他们 INF 文件中指定此值。)

<a href="" id="servicebinary-path-to-service"></a>**ServiceBinary**=*path-to-service*  
指定的服务，表示为二进制文件的路径 *%dirid%\\文件名*。

*Dirid*数是自定义目录标识符或之一中所述的系统定义的目录标识符[使用 Dirids](using-dirids.md)。 给定*文件名*指定一个文件已传输 (请参阅[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)) 从到目标上的目录的源分发媒体计算机。

<a href="" id="startname-driver-object-name"></a>**StartName**=*driver-object-name*  
此可选项指定该驱动程序对象，表示此设备/驱动程序的名称。 如果*类型代码*指定**1** (SERVICE_KERNEL_DRIVER) 或**2** (SERVICE_FILE_SYSTEM_DRIVER)，此名称是 I/O 管理器使用加载的驱动程序对象名称驱动程序。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg**=*添加注册表部分*\[ **，** <em>添加注册表部分</em>\]...  
引用了一个或多 INF 编写器的定义*添加注册表部分*中的任何新安装的服务相关的注册表信息设置。 **HKR**在此类规范*添加注册表部分*指定**HKLM\\系统\\CurrentControlSet\\服务\\ServiceName**注册表项。 有关详细信息，请参阅[ **INF AddReg 指令**](inf-addreg-directive.md)。

此指令很少使用服务安装部分中。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg**=*del 注册表部分*\[ **，** <em>del 注册表部分</em>\]...  
引用了一个或多 INF 编写器的定义*del 注册表部分*哪些相关的注册表中删除已安装的服务的信息。 **HKR**在此类规范*del 注册表部分*指定**HKLM\\系统\\CurrentControlSet\\服务\\ServiceName**注册表项。 有关详细信息，请参阅[ **INF DelReg 指令**](inf-delreg-directive.md)。

在几乎不会使用此指令*服务安装部分*，但它可能会在"更新"以前已安装的相同的设备/驱动程序服务注册表 INF 中使用。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg**=*位注册表部分*\[ **，** <em>位注册表部分</em>\]...  
在中的有效*服务安装部分*但几乎从未使用过。 **HKR**在此类规范*位注册表部分*还会指定**HKLM\\系统\\CurrentControlSet\\服务\\ServiceName**注册表项。

<a href="" id="loadordergroup-load-order-group-name"></a>**LoadOrderGroup**=*load-order-group-name*  
此可选条目标识此驱动程序是其成员之一的加载顺序组。 它可以是一个"标准"的加载顺序组，如**SCSI**类或**NDIS**。

一般情况下，此条目是不必要的以独占方式即插即用设备，或使用 WDM 驱动程序的设备，除非此类组上有旧的依赖项。 但是，此项可以是通过加载一组特定的顺序中的驱动程序支持设备检测的情况下很有用。

有关详细信息**LoadOrderGroup**，请参阅[指定驱动程序加载顺序](specifying-driver-load-order.md)。

<a href="" id="dependencies-depend-on-item-name--depend-on-item-name----"></a>**依赖项**=*依赖-上的项的名称*\[ **，** <em>依赖-上的项的名称</em>\]...  
每个*依赖的上项的名称-* 依赖项列表中的项指定的设备/驱动程序所依赖的服务或加载顺序组名称。

如果*依赖的上项的名称-* 指定的服务，必须在启动此驱动程序之前运行的服务。 例如，对系统提供 Win32 TCP/IP 打印服务 INF 取决于基础 （内核模式） TCP/IP 传输堆栈的支持。 因此，对 TCP/IP 打印服务 INF 指定此项作为**依赖项 = TCPIP**。

一个*依赖的上项的名称-* 可以指定此设备/驱动程序所依赖的加载顺序组。 仅当至少一个指定组的成员启动，启动这样的驱动程序。 组名称前面加上加号 （+）。 例如，系统 RAS 服务 INF 可能如下所示的条目**依赖项 = + NetBIOSGroup，RpcSS**加载顺序组和服务，它列出。

<a href="" id="security--security-descriptor-string-"></a>**Security**="*security-descriptor-string*"  
指定要应用于服务的安全描述符。 此安全说明符指定执行诸如启动、 停止和配置服务所需的权限。 *安全描述符字符串*值是标记，则指示 DACL 的字符串 (**d:** ) 安全组件。

有关安全描述符字符串的信息，请参阅[安全描述符定义语言 (Windows)](https://docs.microsoft.com/windows/desktop/SecAuthZ/security-descriptor-definition-language)。 有关的安全描述符字符串格式的信息，请参阅安全描述符定义语言 (Windows)。

有关如何指定安全描述符的详细信息，请参阅[创建安全的设备安装](creating-secure-device-installations.md)。

### <a name="specifying-driver-load-order"></a>指定驱动程序加载顺序

操作系统加载驱动程序，根据*服务安装部分*  **StartType**值，按如下所示：

-   在系统启动开始阶段，操作系统将加载所有**0x0** (SERVICE_BOOT_START) 驱动程序。
-   在系统启动阶段，操作系统首次加载所有 WDM 和 PnP 管理器为其查找设备节点的即插即用驱动程序 (*devnodes*) 在注册表中 **...\\Enum**树 (其 INF 文件用于指定是否**0x01**为 SERVICE_SYSTEM_START 或**0x03** SERVICE_DEMAND_START 的)。然后加载所有剩余 SERVICE_SYSTEM_START 驱动程序的操作系统。
-   在系统自动启动阶段，操作系统将加载所有剩余 SERVICE_AUTO_START 驱动程序。

有关详细信息**依赖项**，请参阅[指定驱动程序加载顺序](specifying-driver-load-order.md)。

### <a name="promoting-a-drivers-starttype-at-boot-depending-on-boot-scenario"></a>升级在具体取决于引导方案的启动驱动程序的启动类型

根据启动方案中，您可以使用**BootFlags**注册表值以控制时应将操作系统升级的驱动程序**StartType**为 0x0 (SERVICE_BOOT_START) 的值。 你可以指定一个或多个 （或运算） 的以下数字值，表示为十六进制值：

-   0x1 (CM_SERVICE_NETWORK_BOOT_LOAD) 指示应将其升级驱动程序，是否从网络启动。

-   0x2 (CM_SERVICE_VIRTUAL_DISK_BOOT_LOAD) 指示应将其升级驱动程序，是否从 VHD 启动。

-   0x4 (CM_SERVICE_USB_DISK_BOOT_LOAD) 指示应将其升级到该驱动程序，是否从 USB 磁盘启动。

-   0x8 (CM_SERVICE_SD_DISK_BOOT_LOAD) 指示应将其升级驱动程序，是否从 SD 存储启动。

-   0x10 (CM_SERVICE_USB3_DISK_BOOT_LOAD) 指示应将其升级驱动程序，是否从磁盘上的 USB 3.0 控制器启动。

-   0x20 (CM_SERVICE_MEASURED_BOOT_LOAD) 指示应将其升级驱动程序，是否在启用了标准的引导时启动。

-   0x40 (CM_SERVICE_VERIFIER_BOOT_LOAD) 指示应将其升级驱动程序，是否通过已启用的验证程序启动启动。

-   0x80 (CM_SERVICE_WINPE_BOOT_LOAD) 指示应将其升级驱动程序，是否启动到 WinPE。

*服务安装部分*具有以下常规形式：

```ini
[service-install-section]
AddReg=add-registry-section
...

[add-registry-section]
HKR,,BootFlags,0x00010003,0x14 ; CM_SERVICE_USB3_DISK_BOOT_LOAD|CM_SERVICE_USB_DISK_BOOT_LOAD
```

### <a name="registering-for-event-logging"></a>正在注册的事件日志记录

**AddService**指令还可以引用*事件日志-安装部分*INF 文件中的其他位置。 每个此类部分具有以下形式：

```ini
[event-log-install-section]
 
AddReg=add-registry-section[, add-registry-section]... 
[DelReg=del-registry-section[, del-registry-section]...] 
[BitReg=bit-registry-section[,bit-registry-section]...]
 ...
```

对于典型设备/的驱动程序 INF 文件，*事件日志-安装部分*仅使用**AddReg**指令设置驱动程序的事件日志记录消息文件。 **HKR**中的规范*添加注册表部分*指定**HKLM\\系统\\CurrentControlSet\\服务\\EventLog\\** <em>EventLogType</em> **\\** <em>EventName</em>注册表项。 此事件日志记录*添加注册表部分*具有以下常规形式：

```ini
[drivername_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"path\IoLogMsg.dll;path\driver.sys"
HKR,,TypesSupported,0x00010001,7 
```

具体而言，部分中添加两个值项中创建的设备/驱动程序，按如下所示的注册表子项：

-   名为的值条目**EventMessageFile**属于类型[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)FLG_ADDREG_TYPE_EXPAND_SZ 值按指定**0x00020000**。 其值括在双引号 （"）、 将相关联的系统提供*IoLogMsg.dll* （但它无法将另一个日志记录 DLL 相关联） 驱动程序二进制文件。 通常情况下，每个文件的路径，如下所示指定：

    *%%SystemRoot%%\\System32\\IoLogMsg.dll*

    *%%SystemRoot%%\\System32\\drivers\\driver.sys*

-   名为的值条目**类型支持的**属于类型[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)FLG_ADDREG_TYPE_DWORD 值按指定**0x00010001**。

    此值应为驱动程序，请**7**。 此值相当于按位或的 EVENTLOG_SUCCESS、 EVENTLOG_ERROR_TYPE、 EVENTLOG_WARNING_TYPE 和 EVENTLOG_INFORMATION_TYPE，而无需设置 EVENTLOG_AUDIT_*XXX*位。

*事件日志-安装部分*还可以使用[ **DelReg** ](inf-delreg-directive.md)指令以删除以前安装的事件日志消息文件，通过显式删除现有**EventMessageFile**并**类型支持的**值的条目，如果驱动程序二进制文件由新安装的驱动程序将其取代。 (另请参阅[ **INF DelService 指令**](inf-delservice-directive.md)。)

虽然[ **BitReg** ](inf-bitreg-directive.md)指令也是在 INF-编写器定义的有效*事件日志安装*-*部分*，它是几乎从未使用过，因为设备驱动程序事件日志记录的标准值项不是位掩码。

<a name="examples"></a>示例
--------

此示例显示引用的服务安装和事件日志安装各个部分**AddService**指令前面部分中的示例如前面所示[ * **DDInstall *。服务**](inf-ddinstall-services-section.md)。

```ini
[sermouse_Service_Inst]
DisplayName    = %sermouse.SvcDesc%
ServiceType    = 1                   ; = SERVICE_KERNEL_DRIVER
StartType      = 3                   ; = SERVICE_DEMAND_START
ErrorControl   = 1                   ; = SERVICE_ERROR_NORMAL
ServiceBinary  = %12%\sermouse.sys
LoadOrderGroup = Pointer Port

[sermouse_EventLog_Inst]
AddReg = sermouse_EventLog_AddReg

[sermouse_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\IoLogMsg.dll;
       %%SystemRoot%%\System32\drivers\sermouse.sys"
;
; Preceding entry on single line in INF file. Enclosing quotation marks 
; prevent the semicolon from being interpreted as a comment.
;
HKR,,TypesSupported,0x00010001,7

[mouclass_Service_Inst]
DisplayName    = %mouclass.SvcDesc%
ServiceType    = 1                   ; = SERVICE_KERNEL_DRIVER
StartType      = 1                   ; = SERVICE_SYSTEM_START
ErrorControl   = 1                   ; = SERVICE_ERROR_NORMAL
ServiceBinary  = %12%\mouclass.sys
LoadOrderGroup = Pointer Class

[mouclass_EventLog_Inst]
AddReg = mouclass_EventLog_AddReg

[mouclass_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\IoLogMsg.dll;
       %%SystemRoot%%\System32\drivers\mouclass.sys"
HKR,,TypesSupported,0x00010001,7
; ...
[Strings]
; ...
sermouse.SvcDesc = "Serial Mouse Driver"
mouclass.SvcDesc = "Mouse Class Driver"
```

中的引用的示例[ * **DDInstall *。HW** ](inf-ddinstall-hw-section.md)部分中，之前所述，还显示了引用的某些服务安装部分**AddService**指令设置即插即用大写筛选器驱动程序。

## <a name="see-also"></a>请参阅


[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall *。硬件**](inf-ddinstall-hw-section.md)

[***DDInstall*.Services**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

[**DelService**](inf-delservice-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**Strings**](inf-strings-section.md)

 

 






