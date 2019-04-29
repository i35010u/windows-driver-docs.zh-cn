---
title: INF DDInstall.Services 节
description: 每个每个模型 DDInstall.Services 部分包含一个或多个引用的 INF 文件中的其他 INF 编写器定义部分的 INF AddService 指令。
ms.assetid: 30efb094-cc18-4c01-8851-4bc5dba1ae1d
keywords:
- INF DDInstall.Services 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efb03b5b2f1243d6230941206526f119761f4861
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370584"
---
# <a name="inf-ddinstallservices-section"></a>INF DDInstall.Services 节


每个每个模型<em>DDInstall</em>**。服务**部分包含一个或多个[ **INF AddService 指令**](inf-addservice-directive.md)引用 INF 文件中的其他 INF 编写器定义部分。

```ini
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

你可以提供<em>DDInstall</em>**。服务**上至少有一个部分**AddService**指令来控制如何以及何时的特定驱动程序的服务已加载，项目依赖于其他服务或驱动程序，等等。 （可选） 还可以指定事件日志记录服务。

## <a name="entries"></a>条目

<a href="" id="addservice-servicename--flags--service-install-section"></a>
<a href="" id="------------------------------------------------event-log-install-section---eventlogtype---eventname-------"></a>
**AddService =**<em>ServiceName</em>，\[*标志*\]**，**<em>服务安装部分</em>\[，*事件日志-安装部分*\[**，**\[*EventLogType* \] \[ **，**<em>EventName</em>\]\]\]...\]  
此指令引用 INF 编写器的定义*服务安装部分*，并且可能*事件日志-安装部分*其他位置中 INF 文件的设备驱动程序涵盖此*DDInstall*部分。 有关详细信息，请参阅[ **INF AddService 指令**](inf-addservice-directive.md)。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**DelService=**<em>ServiceName</em>\[**,**\[*flags*\]\[**,**\[*EventLogType*\]\[**,**<em>EventName</em>\]\]\]...  
此指令从目标计算机中删除以前安装的服务。 很少使用此指令。 有关详细信息，请参阅[ **INF DelService 指令**](inf-delservice-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include=**<em>filename</em>**.inf**\[**,**<em>filename2</em>**.inf**\]...  
此可选项指定一个或多个其他系统提供 INF 文件包含安装此设备所需的部分。 如果指定此项时，通常那么**需要**条目。

有关详细信息**Include**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需要 =**<em>inf 部分名称</em>\[**，**<em>inf 部分名称</em>\]...  
此可选项指定必须在此设备的安装过程中处理的部分。 通常情况下，部分是<em>DDInstall</em>**。服务**中列出系统提供 INF 文件中的节**Include**条目。 但是，它可以是任何部分中引用的<em>DDInstall</em>**。服务**部分。

**需要**条目不能嵌套。 有关详细信息**需要**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a name="remarks"></a>备注
-------

<em>DDInstall</em>**。服务**部分应具有其相关的相同平台和操作系统修饰[ ***DDInstall*** ](inf-ddinstall-section.md)部分。 例如，<em>安装的部分名称</em>**.ntx86**部分中将具有相应<em>安装部分名称</em>**.ntx86。服务**部分。

指定*DDInstall*部分必须在每个制造商下的特定于设备/模型的项中引用*模型*INF 文件部分。 不区分大小写的扩展*安装的部分名称*所示在正式语法语句可插入到此类<em>DDInstall</em>**。服务**跨平台 INF 文件中的节名称。

有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<a name="examples"></a>示例
--------

此示例演示<em>DDInstall</em>**。服务**部分，了解**Ser_Inst**部分中的示例所示[ **INF *DDInstall*部分**](inf-ddinstall-section.md)。

```ini
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

此示例演示<em>安装的部分名称</em>**。NT。服务**部分，并在 INF 及其服务安装部分文件系统提供 WDM 音频设备/驱动程序的示例所示[ **INF *DDInstall*部分**](inf-ddinstall-section.md).

```ini
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

请参阅[ **INF DDInstall.HW 部分**](inf-ddinstall-hw-section.md)的更多示例<em>DDInstall</em>**。服务**包含一些部分*服务安装*-引用的部分[ **AddService** ](inf-addservice-directive.md)指令。 这包括一个用于即插即用的筛选器驱动程序。

## <a name="see-also"></a>请参阅


[**AddService**](inf-addservice-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。硬件**](inf-ddinstall-hw-section.md)

[**DelService**](inf-delservice-directive.md)

[***模型***](inf-models-section.md)

 

 






