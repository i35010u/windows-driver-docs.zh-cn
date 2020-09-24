---
title: INF AddService 指令
description: AddService 指令用于 INF DDInstall 部分或 INF DefaultInstall 节中。
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
ms.openlocfilehash: ef77d6c136f56f9c24b0839c06e44f783a1cf0c6
ms.sourcegitcommit: 06581a21ca066ddfedab7f9bb7f2159cfac452fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2020
ms.locfileid: "91145453"
---
# <a name="inf-addservice-directive"></a>INF AddService 指令


**注意**   此指令不用于安装不需要任何驱动程序的设备（例如调制解调器或显示器监视器）的 INF 文件。

 

在 INF DDInstall 中使用**AddService**指令[**。 *DDInstall*Services 部分**](inf-ddinstall-services-section.md)或[**INF DefaultInstall 部分**](inf-defaultinstall-services-section.md)。 它指定与驱动程序相关联的服务的特性，如如何和何时加载服务，以及其他基础旧驱动程序或服务的任何依赖项。 此外，此指令还可以为设备设置事件日志记录服务。

```inf
[DDInstall.Services] 
 
AddService=ServiceName,[flags],service-install-section
                     [,event-log-install-section[,[EventLogType][,EventName]]]
...
```

## <a name="entries"></a>项


<a href="" id="servicename"></a>*ServiceName*  
指定要安装的服务的名称。 对于设备，此值通常是其驱动程序的通用名称，如 "sermouse" 或某些此类名称。 此名称不能本地化。 无论系统的本地语言如何，它都必须相同。

<a href="" id="flags"></a>*随意*  
指定在 *setupapi.log*中定义的以下系统定义的运算的一个或多个 () ，表示为十六进制值：

<a href="" id="0x00000001--spsvcinst-tagtofront-"></a>**0x00000001** (SPSVCINST_TAGTOFRONT)   
将命名服务的标记移到其组顺序列表的前面，以确保在该组中第一次加载该服务的标记 (除非随后使用此 INF 规范安装的设备视角它) 。 通过 WDM 驱动程序安装专用设备和设备的 INF 文件不应设置此标志。

<a href="" id="0x00000002--spsvcinst-assocservice-"></a>**0x00000002** (SPSVCINST_ASSOCSERVICE)   
将命名服务指定为该 INF 文件所安装的设备的 PnP 函数驱动程序 (或旧驱动程序) 。

若要指示服务是设备的函数驱动程序，服务应在**AddService**指令中指定**SPSVCINST_ASSOCSERVICE**标志。  对于筛选器驱动程序或其他驱动程序组件等服务，不应使用标志。

每个设备驱动程序 INF 应该只有一个关联的服务。  INF 不需要关联的服务（如果它是扩展）或使用 Include/需求指令从另一个 INF 继承关联的服务。  对于不需要函数驱动程序的设备，可以按如下所示指定 NULL 驱动程序：

```
AddService = ,2.
```

<a href="" id="0x00000008--spsvcinst-noclobber-displayname-"></a>**0x00000008** (SPSVCINST_NOCLOBBER_DISPLAYNAME)   
如果系统中已存在此服务，请不要覆盖给定服务的 (可选) 友好名称。

<a href="" id="0x00000010--spsvcinst-noclobber-starttype-"></a>**0x00000010** (SPSVCINST_NOCLOBBER_STARTTYPE)   
如果系统中已存在此命名服务，则不会覆盖给定服务的启动类型。

<a href="" id="0x00000020--spsvcinst-noclobber-errorcontrol-"></a>**0x00000020** (SPSVCINST_NOCLOBBER_ERRORCONTROL)   
如果系统中已存在此命名服务，则不要覆盖给定服务的错误控制值。

<a href="" id="0x00000040--spsvcinst-noclobber-loadordergroup-"></a>**0x00000040** (SPSVCINST_NOCLOBBER_LOADORDERGROUP)   
如果系统中已存在此命名服务，则不要覆盖给定服务的加载顺序组值。 通过 WDM 驱动程序安装专用设备和设备的 INF 文件不应设置此标志。

<a href="" id="0x00000080--spsvcinst-noclobber-dependencies--"></a>**0x00000080** (SPSVCINST_NOCLOBBER_DEPENDENCIES)    
如果系统中已存在此命名服务，则不要覆盖给定服务的依赖项列表。 通过 WDM 驱动程序安装专用设备和设备的 INF 文件不应设置此标志。

<a href="" id="0x00000100--spsvcinst-noclobber-description-"></a>**0x00000100** (SPSVCINST_NOCLOBBER_DESCRIPTION)   
如果系统中已存在此服务，请不要覆盖给定服务的 (可选) 描述。

<a href="" id="0x00000400--spsvcinst-clobber-security---windows-xp-and-later-versions-of-windows--"></a>**0x00000400** (SPSVCINST_CLOBBER_SECURITY)  (windows XP 和更高版本的 windows)    
如果系统中已存在此服务，则覆盖该服务的安全设置。

<a href="" id="0x00000800--spsvcsinst-startservice---windows-vista-and-later-versions-of-windows--"></a>**0x00000800** (SPSVCSINST_STARTSERVICE)  (windows Vista 和更高版本的 windows)    
安装服务后，启动服务。 此标志不能用于启动为设备实现即插即用 (PnP) 函数驱动程序或筛选器驱动程序的服务。 否则，此标志可用于启动由服务控制管理器 (SCM) 管理的用户模式或内核模式服务。

<a href="" id="0x00001000--spsvcinst-noclobber-requiredprivileges---windows-7-and-later-versions-of-windows-"></a>**0x00001000** (SPSVCINST_NOCLOBBER_REQUIREDPRIVILEGES)  (windows 7 和更高版本的 windows)   
如果系统中已存在该服务，则不会覆盖给定服务的权限。

<a href="" id="service-install-section"></a>*服务-安装-部分*  
引用由 INF 写入方定义的部分，其中包含为此设备 (或设备) 安装命名服务的信息。 有关详细信息，请参阅下面的 " **备注** " 部分。

<a href="" id="event-log-install-section"></a>*事件日志-安装-部分*  
（可选）引用由 INF 写入方定义的部分，在此部分中，将对此设备 (的事件日志记录服务，或) 设置设备。

<a href="" id="eventlogtype"></a>*EventLogType*  
根据需要指定 **系统**、 **安全**或 **应用程序**之一。 如果省略，则默认为 **System**，这几乎始终是安装设备驱动程序的适当值。

例如，如果要安装的驱动程序提供其自己的安全支持，则 INF 仅指定 **安全性** 。

<a href="" id="eventname"></a>*名*  
（可选）指定要用于事件日志的名称。 如果省略，则默认为给定的 *ServiceName*。

<a name="remarks"></a>备注
-------

系统定义和不区分大小写的扩展可以插入 <em>DDInstall</em>**。服务** 部分，其中包含跨操作系统系统和/或跨平台 INF 文件中的 **AddService** 指令，用于指定特定于平台或特定于操作系统的安装。

在 INF 文件中，每个 INF 编写器创建的节名称必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

**AddService**指令必须在 INF 文件中的其他位置引用命名*服务安装部分*。 每个此类部分都具有以下形式：

```inf
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
[ServiceSidType=value]
[DelayedAutoStart=true/false]
[AddTrigger=service-trigger-install-section[, service-trigger-install-section, ...]]
```

每个 *服务安装部分* 必须至少有 **ServiceType**、 **StartType**、 **ErrorControl**和 **ServiceBinary** 项，如下所示。 但是，其余条目是可选的。

### <a name="service-install-section-entries-and-values"></a>服务-安装节项和值

<a href="" id="displayname-name"></a>**DisplayName** =*名称*  
为服务/驱动程序指定一个友好名称，通常为简化本地化，表示为在 INF 文件的[**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌。

<a href="" id="description-description-string"></a>**描述** =*description-字符串*  
（可选）指定描述服务的字符串，通常表示为在 INF 文件的**字符串**部分中定义的%*strkey*% 令牌。

此字符串为用户提供有关该服务的详细信息，而不是 **DisplayName**。 例如， **DisplayName** 的名称可能类似于 "DHCP 客户端"，描述可能类似于 "通过注册和更新 IP 地址和 DNS 名称来管理网络配置"。

*说明字符串*的长度应足以区分描述性，但不要太长。 如果 *说明字符串* 包含任何%*strkey*% 令牌，则每个令牌最多可以表示511个字符。 所有字符串标记替换后的总字符串不应超过1024个字符。

<a href="" id="servicetype-type-code"></a>**ServiceType** =*类型代码*  
内核模式设备驱动程序的类型代码必须设置为 0x00000001 (SERVICE_KERNEL_DRIVER) 。

为设备安装的 Microsoft Win32 服务的 *类型代码* 应该设置为 **0x00000010** (SERVICE_WIN32_OWN_PROCESS) 或 **0x00000020** (SERVICE_WIN32_SHARE_PROCESS) 。 如果 Win32 服务可与桌面交互，则应将类型代码值与 **0x00000100** (SERVICE_INTERACTIVE_PROCESS) 结合。

最高级别网络驱动程序的 *类型代码* （例如，重定向程序或文件系统驱动程序）应设置为 **0x00000002** (SERVICE_FILE_SYSTEM_DRIVER) 。

在 *Wdm .h* 和 *Ntddk*中定义 SERVICE_xxxx 常量。

<a href="" id="starttype-start-code"></a>**StartType** =*开始-代码*  
指定何时启动驱动程序作为以下数值之一（用 decimal 或表示），如下面的列表所示，采用十六进制表示法。

<a href="" id="0x0--service-boot-start-"></a>**0x0** (SERVICE_BOOT_START)   
指示由操作系统加载程序启动的驱动程序。

此值必须用于加载操作系统所需的设备驱动程序。

<a href="" id="0x1--service-system-start-"></a>**0x1** (SERVICE_SYSTEM_START)   
指示在操作系统初始化期间启动了驱动程序。

此值应该由 PnP 驱动程序使用，该驱动程序在初始化期间进行设备检测，但不需要加载系统。

例如，可以检测到旧设备的 PnP 驱动程序应在其 INF 中指定此值，以便调用其 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程查找旧设备，即使该设备无法由 PnP 管理器枚举。

<a href="" id="0x2--service-auto-start-"></a>**0x2** (SERVICE_AUTO_START)   
指示在系统启动期间由服务控制管理器启动的驱动程序。

此值绝不能用于 WDM 或 PnP 设备驱动程序的 INF 文件。

<a href="" id="0x3--service-demand-start-"></a>**0x3** (SERVICE_DEMAND_START)   
指示当服务控制管理器对非 PnP 设备的显式用户需求进行枚举或服务控制管理器时，按需启动驱动程序。

对于不需要加载系统的设备的所有 WDM 驱动程序以及加载系统和参与设备检测所需的所有 PnP 设备驱动程序，此值应在 INF 文件中使用。

<a href="" id="0x4--service-disabled-"></a><strong>0x4 (</strong>SERVICE_DISABLED)   
指示无法启动的驱动程序。

此值可用于暂时禁用设备的驱动程序服务。 但是，如果在其 INF 文件的 "服务安装" 部分中指定了此值，则无法安装该设备/驱动程序。

有关 **StartType**的详细信息，请参阅 [指定驱动程序加载顺序](specifying-driver-load-order.md)。

<a href="" id="errorcontrol-error-control-level"></a>**ErrorControl** =*错误-控件级别*  
以十六进制表示法，将错误控制级别指定为以下数字值之一（用 decimal 或表示），如下面的列表所示。

<a href="" id="0x0--service-error-ignore-"></a>**0x0** (SERVICE_ERROR_IGNORE)   
如果驱动程序无法加载或初始化，请继续系统启动并不向用户显示警告。

<a href="" id="0x1--service-error-normal-"></a>**0x1** (SERVICE_ERROR_NORMAL)   
如果驱动程序无法加载或初始化其设备，系统会继续进行，但会向用户显示一条警告。

<a href="" id="0x2--service-error-severe-"></a>**0x2** (SERVICE_ERROR_SEVERE)   
如果驱动程序未能加载，则系统启动应切换到注册表的 **LastKnownGood** 控制集，并继续系统启动，即使驱动程序再次指示加载或设备/驱动程序初始化错误也是如此。

<a href="" id="0x3--service-error-critical-"></a>**0x3** (SERVICE_ERROR_CRITICAL)   
如果无法加载驱动程序，并且系统启动未使用注册表的 **LastKnownGood** 控制集，请切换到 **LastKnownGood** 并重试。

如果在使用 **LastKnownGood**时启动仍失败，请运行 bug 检查例程。 *仅* (系统启动所需的设备/驱动程序在其 INF 文件中指定此值。 ) 

<a href="" id="servicebinary-path-to-service"></a>**ServiceBinary** =*路径到服务*  
指定服务的二进制文件的路径，表示为 *% dirid% \\ filename*。

*Dirid*号可以是自定义目录标识符，也可以是[使用 Dirids](using-dirids.md)中所述的系统定义的目录标识符之一。 给定的 *文件名* 指定已传输的文件 (参阅 [**INF CopyFiles 指令**](inf-copyfiles-directive.md)) 从源分发媒体到目标计算机上的目录。

<a href="" id="startname-driver-object-name"></a>**StartName** =*驱动程序-对象名称*  
此可选条目指定表示此设备/驱动程序的驱动程序对象的名称。 如果 *类型代码* 指定 **1** (SERVICE_KERNEL_DRIVER **) 或 SERVICE_FILE_SYSTEM_DRIVER** () ，则此名称是 i/o 管理器用来加载驱动程序的驱动程序对象名称。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg** =*添加-注册表-部分* \[**，**<em>添加-注册表-节</em> \] .。。  
引用一个或多个 INF 写入器定义的 *外* 接程序，其中设置了与新安装的服务相关的任何注册表信息。 此类 " **HKR** " *部分* 指定了 **HKLM \\ System \\ CurrentControlSet \\ Services \\ ServiceName** 注册表项。 有关详细信息，请参阅 [**INF AddReg 指令**](inf-addreg-directive.md)。

此指令很少用于服务安装部分。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg** =*del-registry-部分* \[**，**<em>del-registry-节</em> \] .。。  
引用一个或多个由 INF 写入器定义的 " *del-注册表" 部分* ，其中已删除已安装服务的相关注册表信息。 这种 **HKR** 规范在这种 " *del-registry" 部分* 中指定了 **HKLM \\ System \\ CurrentControlSet \\ Services \\ ServiceName** 注册表项。 有关详细信息，请参阅 [**INF DelReg 指令**](inf-delreg-directive.md)。

此指令几乎不能用于 *服务安装部分*，但它可能用于 "更新" 注册表以用于以前安装的相同设备/驱动程序服务。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg** =*位注册表-部分* \[**，**<em>位注册表-节</em> \] .。。  
在 *服务安装部分* 有效，但几乎从未使用过。 此类*注册表部分*中的**HKR**规范还指定了**HKLM \\ System \\ CurrentControlSet \\ Services \\ ServiceName**注册表项。

<a href="" id="loadordergroup-load-order-group-name"></a>**LoadOrderGroup** =*加载顺序-组名称*  
此可选条目用于标识此驱动程序所属的加载顺序组。 它可以是 "标准" 加载顺序组（如 **SCSI** 类或 **NDIS**）之一。

一般情况下，除非此类组有旧依赖项，否则对于具有 WDM 驱动程序的设备或独占 PnP 设备，此项不是必需的。 但是，如果支持通过按特定顺序加载一组驱动程序来支持设备检测，则此项会很有用。

有关 **LoadOrderGroup**的详细信息，请参阅 [指定驱动程序加载顺序](specifying-driver-load-order.md)。

<a href="" id="dependencies-depend-on-item-name--depend-on-item-name----"></a>**依赖关系** =*依赖项-名称* \[**，**<em>依赖项-名称</em> \] .。。  
依赖项列表中的每个 *项依赖项名称* 项指定了设备/驱动程序所依赖的服务或加载顺序组的名称。

如果 *依赖项名称* 指定了服务，则在启动此驱动程序之前必须运行该服务。 例如，系统提供的 Win32 TCP/IP 打印服务的 INF 依赖于基础 (内核模式) TCP/IP 传输堆栈的支持。 因此，TCP/IP 打印服务的 INF 将此项指定为 **依赖项**。

*依赖项名称*可以指定此设备/驱动程序所依赖的加载顺序组。 仅当启动指定组中的至少一个成员时，才会启动此类驱动程序。 在组名称之前加上加号 (+) 。 例如，系统 RAS 服务 INF 可能有一个类似于 **"NetBIOSGroup"** 的条目，其中列出了负载顺序组和服务。

<a href="" id="security--security-descriptor-string-"></a>**Security**= "*security-描述符-string*"  
指定要应用于服务的安全描述符。 此安全描述符指定执行此类操作（如启动、停止和配置服务）所需的权限。 *安全描述符字符串*值是带有标记的字符串，用于指示 DACL (**D：**) 安全组件。

有关安全描述符字符串的信息，请参阅 [安全描述符定义语言 (Windows) ](/windows/desktop/SecAuthZ/security-descriptor-definition-language)。 有关安全描述符字符串的格式的信息，请参阅安全描述符定义语言 (Windows) 。

有关如何指定安全描述符的详细信息，请参阅 [创建安全设备安装](creating-secure-device-installations.md)。

<a href="" id="description-description-string"></a>**ServiceSidType** =*值*

**注意：** 此值仅可用于 *Win32 服务* ，且仅适用于 Windows 10 版本2004及更高版本。

此项可以使用 [SERVICE_SID_INFO](/windows/win32/api/winsvc/ns-winsvc-service_sid_info)中所述的任何有效值。

<a href="" id="description-description-string"></a>**DelayedAutoStart** =*true/false*

**注意：** 此值仅可用于 *Win32 服务* ，且仅适用于 Windows 10 2004 及更高版本。

包含自动启动服务的延迟自动启动设置。

如果此成员为 TRUE，则在启动其他自动启动服务并出现短暂延迟后，将启动该服务。 否则，该服务将在系统启动期间启动。

此设置将被忽略，除非该服务是自动启动服务。

有关详细信息，请参阅 [本页](/windows/win32/api/winsvc/ns-winsvc-service_delayed_auto_start_info)。

<a href="" id="description-description-string"></a>**AddTrigger** =*服务触发器-安装部分 [，服务触发器-安装节，...]*

指定要为 Win32 服务注册的触发器事件，以便在发生触发器事件时可以启动或停止该服务。 有关服务触发器事件的详细信息，请参阅 [服务触发器事件](/windows/desktop/Services/service-trigger-events)。

AddTrigger 指令引用的每个命名的服务触发器安装部分均采用以下格式：

```
[service-trigger-install-section]

TriggerType=trigger-type
Action=action-type
SubType=trigger-subtype
[DataItem=data-type,data]
...
```

### <a name="service-trigger-install-section-entries-and-values"></a>服务触发器-安装节项和值：
**TriggerType** =*触发器类型*

按照以下列表中所示的十六进制表示法，用以下数字值之一指定服务触发器事件类型：

**0x1** (SERVICE_TRIGGER_TYPE_DEVICE_INTERFACE_ARRIVAL) 指示在系统启动时，指定设备接口类的设备到达或存在时触发事件。 

有关详细信息，请参阅 [SERVICE_TRIGGER 结构](/windows/win32/api/winsvc/ns-winsvc-service_trigger)

**操作** =*操作-类型*

指定发生指定的触发器事件时要执行的操作。

**0x1** (SERVICE_TRIGGER_ACTION_SERVICE_START) 在指定的触发事件发生时启动服务。

**0x2** (SERVICE_TRIGGER_ACTION_SERVICE_STOP) 在指定的触发事件发生时停止服务。

有关详细信息，请参阅 [SERVICE_TRIGGER 结构](/windows/win32/api/winsvc/ns-winsvc-service_trigger)

**子类型** =*触发器-子类型*

指定标识 trigger 事件子类型的 GUID。 该值取决于 **TriggerType**的值。 

当 **TriggerType** 为 **0x1** 时 (SERVICE_TRIGGER_TYPE_DEVICE_INTERFACE_ARRIVAL) ， **子类型** 指定标识设备接口类的 GUID。

有关详细信息，请参阅 [SERVICE_TRIGGER 结构](/windows/win32/api/winsvc/ns-winsvc-service_trigger)。

**DataItem** =*数据类型，数据*

（可选）指定服务触发器事件的触发器特定数据。 

当 **TriggerType** 为 **0x1** (SERVICE_TRIGGER_TYPE_DEVICE_INTERFACE_ARRIVAL) 时，可以使用数据类型 **0X2** (指定可选的 DataItem，SERVICE_TRIGGER_DATA_TYPE_STRING) 将设备接口类的范围限定为特定硬件 id 或兼容 ID。

有关详细信息，请参阅 [SERVICE_TRIGGER_SPECIFIC_DATA_ITEM 结构](/windows/win32/api/winsvc/ns-winsvc-service_trigger_specific_data_item)

使用 **AddTrigger** 指令的最佳做法是在设备接口到达时触发服务的启动。 有关详细信息，请参阅 [Win32 服务与设备交互](./best-practices-win32services-interacting-with-devices.md)。

**注意： AddTrigger** 语法仅适用于 **Windows 10 版本 2004** 和更转发版。


### <a name="specifying-driver-load-order"></a>指定驱动程序加载顺序

操作系统根据  **StartType**值加载驱动程序，*如下所示*：

-   在系统启动开始阶段，操作系统 SERVICE_BOOT_START) 驱动程序加载所有 **0x0** (。
-   在系统启动阶段，操作系统会首先加载 PnP 管理器找到其设备节点 *)  (的*所有 WDM 和 PnP 驱动程序 **。 \\枚举**树 (其 INF 文件是否为 SERVICE_DEMAND_START) 的 SERVICE_SYSTEM_START 或**0x03**指定**0x01** 。然后，操作系统会加载所有剩余的 SERVICE_SYSTEM_START 驱动程序。
-   在系统自动启动阶段，操作系统会加载所有剩余的 SERVICE_AUTO_START 驱动程序。

有关 **依赖关系**的详细信息，请参阅 [指定驱动程序加载顺序](specifying-driver-load-order.md)。

### <a name="promoting-a-drivers-starttype-at-boot-depending-on-boot-scenario"></a>在启动时根据启动方案升级驱动程序的 StartType

根据启动方案，可以使用 **BootFlags** 注册表值来控制操作系统应将驱动程序的 **StartType** 值升级为 0x0 (SERVICE_BOOT_START) 。 可以指定以下数值的一个或多个 (运算) ，以十六进制值表示：

-   0x1 (CM_SERVICE_NETWORK_BOOT_LOAD) 指示在从网络启动时应升级的驱动程序。

-   0x2 (CM_SERVICE_VIRTUAL_DISK_BOOT_LOAD) 指示当从 VHD 启动时应升级驱动程序。

-   0x4 (CM_SERVICE_USB_DISK_BOOT_LOAD) 指示在从 USB 磁盘启动时应将驱动程序升级到。

-   0x8 (CM_SERVICE_SD_DISK_BOOT_LOAD) 指示从 SD 存储启动时应升级的驱动程序。

-   0x10 (CM_SERVICE_USB3_DISK_BOOT_LOAD) 指示在从 USB 3.0 控制器上的磁盘启动时应升级的驱动程序。

-   0x20 (CM_SERVICE_MEASURED_BOOT_LOAD) 指示当启用标准启动时启动时应升级驱动程序。

-   0x40 (CM_SERVICE_VERIFIER_BOOT_LOAD) 指示在启用了验证程序启动的情况启动时应升级驱动程序。

-   0x80 (CM_SERVICE_WINPE_BOOT_LOAD) 指示在启动到 WinPE 时应升级驱动程序。

" *服务安装" 部分* 具有以下通用格式：

```inf
[service-install-section]
AddReg=add-registry-section
...

[add-registry-section]
HKR,,BootFlags,0x00010003,0x14 ; CM_SERVICE_USB3_DISK_BOOT_LOAD|CM_SERVICE_USB_DISK_BOOT_LOAD
```

### <a name="registering-for-event-logging"></a>注册事件日志记录

**AddService**指令还可在 INF 文件中的其他位置引用*事件日志安装部分*。 每个此类部分都具有以下形式：

```inf
[event-log-install-section]
 
AddReg=add-registry-section[, add-registry-section]... 
[DelReg=del-registry-section[, del-registry-section]...] 
[BitReg=bit-registry-section[,bit-registry-section]...]
 ...
```

对于典型的设备/驱动程序 INF 文件， *事件日志-安装部分* 仅使用 **AddReg** 指令为驱动程序设置事件日志记录文件。 "*添加注册表" 一节*中的**HKR**规范指定**HKLM \\ System \\ CurrentControlSet \\ Services \\ EventLog \\ **<em>EventLogType</em> **\\** <em>事件</em>日志项。 此事件日志记录 *添加注册表部分* 具有以下常规形式：

```inf
[drivername_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"path\IoLogMsg.dll;path\driver.sys"
HKR,,TypesSupported,0x00010001,7 
```

特别是，部分在为设备/驱动程序创建的注册表子项中添加了两个值项，如下所示：

-   名为 **EventMessageFile** 的值项的类型为 [REG_EXPAND_SZ](/windows/desktop/SysInfo/registry-value-types)，由 FLG_ADDREG_TYPE_EXPAND_SZ 值 **0x00020000**指定。 其值括在双引号 ( ") 中，它将系统提供的 *IoLogMsg.dll* 相关联 (但它可以将其他日志记录 DLL) 与驱动程序二进制文件相关联。 通常，按如下所示指定每个文件的路径：

    *%% SystemRoot%% \\ System32 \\IoLogMsg.dll*

    *%% SystemRoot%% \\ System32 \\ 驱动程序 \\driver.sys*

-   名为 **TypesSupported** 的值项的类型为 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types)，由 FLG_ADDREG_TYPE_DWORD 值 **0x00010001**指定。

    对于驱动程序，此值应为 **7**。 此值等效于 EVENTLOG_SUCCESS、EVENTLOG_ERROR_TYPE、EVENTLOG_WARNING_TYPE 和 EVENTLOG_INFORMATION_TYPE 的按位 "或"，而不设置 EVENTLOG_AUDIT_*XXX* 位。

如果新安装的驱动程序正在取代驱动程序二进制文件 *，则还可以使用* [**DelReg**](inf-delreg-directive.md) 指令删除以前安装的事件日志消息文件，方法是显式删除现有的 **EventMessageFile** 和 **TypesSupported** 值项。  (另请参阅 [**INF DelService 指令**](inf-delservice-directive.md)。 ) 

尽管[**BitReg**](inf-bitreg-directive.md)指令在 INF-编写器定义的*事件日志安装* - *部分*中也有效，但它几乎从未使用过，因为设备驱动程序事件日志记录的标准值项不是位掩码。

<a name="examples"></a>示例
--------

此示例显示了**AddService**指令引用的服务安装和事件日志-安装部分，如[ * DDInstall * 的示例中所示 **。服务**](inf-ddinstall-services-section.md)。

```inf
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

DDInstall * 的参考中的示例[ * **。**](inf-ddinstall-hw-section.md)前面所述的 HW 部分还显示了**AddService**指令所引用的某些服务安装部分，以设置 PnP 上层筛选器驱动程序。

## <a name="see-also"></a>另请参阅


[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall*.HW**](inf-ddinstall-hw-section.md)

[***DDInstall*.服务器**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

[**DelService**](inf-delservice-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**字符串**](inf-strings-section.md)

 

