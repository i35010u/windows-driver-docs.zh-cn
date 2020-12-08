---
title: INF DDInstall.Services 节
description: 每个模型的 DDInstall 节都包含一个或多个 INF AddService 指令，这些指令引用 INF 文件中其他由 INF 编写器定义的部分。
keywords:
- INF DDInstall 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b57a47bcd10180eb9fc5c23c2a5b93c3fbdbc739
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787437"
---
# <a name="inf-ddinstallservices-section"></a>INF DDInstall.Services 节


每个模型 <em>DDInstall</em>**。Services** 节包含一个或多个 [**inf AddService 指令**](inf-addservice-directive.md) ，这些指令引用 inf 文件中其他由 inf 编写器定义的部分。

```inf
[install-section-name.Services] |
[install-section-name.nt.Services] |
[install-section-name.ntx86.Services] |
[install-section-name.ntarm.Services] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.Services] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.Services] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.Services]  (Windows XP and later versions of Windows)
 
AddService=ServiceName,[flags],service-install-section
                     [,event-log-install-section[,[EventLogType][,EventName]]]...]
[DelService=ServiceName[,[flags][,[EventLogType][,EventName]]]]...
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...] 
```

可以提供 <em>DDInstall</em>**。** 包含至少一个 **AddService** 指令的服务部分，用于控制加载特定驱动程序的服务的方式和时间、其他服务或驱动程序的依赖关系等。 还可以选择指定事件日志记录服务。

## <a name="entries"></a>项

<a href="" id="addservice-servicename--flags--service-install-section"></a>
<a href="" id="------------------------------------------------event-log-install-section---eventlogtype---eventname-------"></a>
**AddService =**<em>ServiceName</em>， \[ *flags* \] **，**<em>service-</em>安装节， \[ *事件日志-安装节* \[ **，** \[ *EventLogType* \] \[ **，** 事件<em>名称</em> \] \] \] .。。\]  
此指令在 INF 文件中 *的其他位置* 引用了一个由 inf 编写器定义的 *服务安装部分*，也可能是在此 *DDInstall* 部分所涵盖的设备的驱动程序的 inf 文件中的其他地方。 有关详细信息，请参阅 [**INF AddService 指令**](inf-addservice-directive.md)。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**DelService =**<em>ServiceName</em> \[ **，** \[ *flags* \] \[ **，** \[ *EventLogType* \] \[ **，**<em>事件名称</em> \] \] \] .。。  
此指令从目标计算机中删除以前安装的服务。 此指令很少使用。 有关详细信息，请参阅 [**INF DelService 指令**](inf-delservice-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**.inf** \[ **，**<em>filename2</em>**.inf** \] .。。  
此可选条目指定一个或多个系统提供的其他 INF 文件，其中包含安装此设备所需的部分。 如果指定此项，则通常是 **需要** 输入。

有关其用法的 **包含** 项和限制的详细信息，请参阅 [指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需求 =**<em>inf-名称</em> \[ **，**<em>inf-节名称</em> \] .。。  
此可选条目指定在安装此设备过程中必须处理的部分。 通常，部分是 <em>DDInstall</em>**。** " **包含** 项" 中列出的系统提供的 INF 文件中的 "服务" 部分。 但是，它可以是在 DDInstall 中引用的任何节 <em>DDInstall</em>**。服务** 部分。

不能嵌套 **需求** 条目。 有关其用法的 **需求** 条目和限制的详细信息，请参阅 [指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a name="remarks"></a>备注
-------

<em>DDInstall</em>**。服务** 部分应该与它们相关的 [ * *_DDInstall_* _](inf-ddinstall-section.md)部分具有相同的平台和操作系统修饰。 例如，<em>安装节名称</em>*ntx86** 节会有相应的 <em>安装节名称</em>**. ntx86。服务** 部分。

在 INF 文件的 "每制造商"*型号* 部分下，必须在特定于设备/模型的条目中引用指定的 *DDInstall* 部分。 在正式语法语句中显示的 *安装节名称* 不区分大小写的扩展可以插入到此类 <em>DDInstall</em>中 **。** 跨平台 INF 文件中的服务部分名称。

有关如何使用 **系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm** 和 **Ntarm64** 扩展的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<a name="examples"></a>示例
--------

此示例显示了 <em>DDInstall</em>**。** 作为 [**INF *DDInstall* 部分**](inf-ddinstall-section.md)示例的 " **Ser_Inst** " 部分的 "服务" 部分。

```inf
[Ser_Inst.Services]
AddService=sermouse, 0x00000002, sermouse_Service_Inst,\
                sermouse_EventLog_Inst 
;
; flags value in preceding entry indicates function driver of device
; 
AddService = mouclass,, mouclass_Service_Inst, mouclass_EventLog_Inst 

; entries in the following xxx_Inst sections omitted here for brevity,
; but fully specified as the example for the AddService directive
;
[sermouse_Service_Inst]
; ...

[sermouse_EventLog_Inst]
; ...

[mouclass_Service_Inst]
; ...

[mouclass_EventLog_Inst]
; ...
```

此示例显示了 <em>安装部分的名称</em>**。NT.服务** 部分及其服务-安装节，适用于系统提供的 WDM 音频设备/驱动程序的 inf 文件中，如 [**inf *DDInstall* 部分**](inf-ddinstall-section.md)所示。

```inf
[WDMPNPB003_Device.NT.Services]
AddService = wdmaud,0x00000000,wdmaud_Service_Inst
AddService = swmidi,0x00000000,swmidi_Service_Inst
AddService = sb16,  0x00000002,sndblst_Service_Inst

[wdmaud_Service_Inst]
DisplayName   = %wdmaud.SvcDesc% ; friendly name (see Strings)
ServiceType   = 1                ; SERVICE_KERNEL_DRIVER
StartType     = 1                ; SERVICE_SYSTEM_START
ErrorControl  = 1                ; SERVICE_ERROR_NORMAL
ServiceBinary = %10%\system32\drivers\wdmaud.sys

[swmidi_Service_Inst]
DisplayName   = %swmidi.SvcDesc% 
ServiceType   = 1 
StartType     = 1 
ErrorControl  = 1 
ServiceBinary = %10%\system32\drivers\swmidi.sys

[sndblst_Service_Inst]
DisplayName   = %sndblst.SvcDesc% 
ServiceType   = 1 
StartType     = 1 
ErrorControl  = 1 
ServiceBinary = %10%\system32\drivers\mssb16.sys

[Strings] ; only immediately preceding %strkey% tokens shown here
%wdmaud.SvcDesc%="Microsoft WDM Virtual Wave Driver (WDM)"
%swmidi.SvcDesc%="Microsoft Software Synthesizer (WDM)"
%sndblst.SvcDesc%="WDM Sample Driver for SB16"
```

有关 <em>DDInstall</em>的更多示例，请参阅 [**INF DDInstall 部分**](inf-ddinstall-hw-section.md)**。服务** 节，其中包含 [**AddService**](inf-addservice-directive.md)指令引用的某些 *服务安装* 部分。 这包括一个用于 PnP 筛选器驱动程序。

## <a name="see-also"></a>请参阅


[**AddService**](inf-addservice-directive.md)

[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *_DDInstall_。HW**](inf-ddinstall-hw-section.md)

[**DelService**](inf-delservice-directive.md)

[**_模型_**](inf-models-section.md)

 

 






