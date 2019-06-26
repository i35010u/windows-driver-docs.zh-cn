---
title: INF AddEventProvider 指令
author: andylsn
description: AddEventProvider 指令使用 INF DDInstall.Events 部分内。
ms.assetid: ''
keywords:
- INF AddEventProvider 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF AddEventProvider Directive
api_type:
- NA
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9fd3bbc859f70910e3908e329e61d3d7d81dd538
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385926"
---
# <a name="inf-addeventprovider-directive"></a>INF AddEventProvider 指令

**AddEventProvider**中使用指令[ **INF *DDInstall*。事件部分**](inf-ddinstall-services-section.md)。 指定的特征[Windows 的事件跟踪](https://docs.microsoft.com/windows/desktop/ETW/about-event-tracing)(ETW) 提供程序与驱动程序相关联。 适用于 Windows 10 1809年和更高版本支持此指令。

```ini
[DDInstall.Events] 

AddEventProvider={ProviderGUID},event-provider-install-section
...
```

## <a name="entries"></a>条目


<a href="" id="ProviderGUID"></a>*ProviderGUID*  
指定标识提供程序的 GUID 值。 这可以表示为一个显式的 GUID 值的窗体`{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}`或 %strkey%令牌到定义`{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}`中[**字符串**](inf-strings-section.md) INF 文件部分。

<a href="" id="event-provider-install-section"></a>*event-provider-install-section*  
引用了一个 INF 编写器定义的部分，其中包含用于注册此设备 （或设备） 的提供程序的信息。 有关详细信息，请参阅以下**备注**部分。

<a name="remarks"></a>备注
-------

系统定义的和不区分大小写扩展可以插入到<em>DDInstall</em> **。事件**节，其中包含**AddEventProvider**指令跨操作系统系统和/或跨平台 INF 文件中指定特定于平台的或特定于操作系统的安装。

每个 INF 编写器创建的部分名称的 INF 文件中必须是唯一和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

**AddEventProvider**指令必须引用一个已命名*事件提供程序安装部分*INF 文件中的其他位置。 每个此类部分具有以下形式：

```ini
[event-provider-install-section]
 
ProviderName=name
ResourceFile=path-to-file
[MessageFile=path-to-file]
[ParameterFile=path-to-file]
(ImportChannel=channel-name) |
(AddChannel=channel-name,channel-type[,channel-install-section])
...
```

每个*事件提供程序安装部分*必须提供**ProviderName**并**ResourceFile**。 （可选） 提供程序使用的任意组合指定的信道列表**ImportChannel(s)** 并**AddChannel(s)** ，每个单独的行上。 有关 INF 文件中的通道列表的详细信息，请参阅[**指定通道列表**](#specifying-a-channel-list)下面。 有关详细信息[Windows 事件日志](https://docs.microsoft.com/windows/desktop/WES/windows-event-log)通道，请参阅[定义通道](https://docs.microsoft.com/windows/desktop/WES/defining-channels)。

### <a name="event-provider-install-section-entries-and-values"></a>事件提供程序安装节条目和值

<a href="" id="providername-name"></a>**ProviderName**=*name*  
指定的提供程序名称。 名称长度不能超过 255 个字符，并且不能包含字符: >，<，&、"，|、\'，:，' '，'？ '，*，或与 ASCII 字符的值小于 31。 此外，该名称必须遵循文件和注册表项名称的常规约束。 这些约束，请参阅[为文件命名](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file)并[注册表元素大小限制](https://docs.microsoft.com/windows/desktop/SysInfo/registry-element-size-limits)。

<a href="" id="resourcefile-path-to-file"></a>**ResourceFile**=*path-to-file*  
指定的 exe 或 dll，其中包含表示为 %dirid%\filename 的提供程序的元数据资源的路径。

*Dirid*数是自定义目录标识符或之一中所述的系统定义的目录标识符[使用 Dirids](using-dirids.md)。

<a href="" id="messagefile-path-to-file"></a>**MessageFile**=*path-to-file*  
（可选） 指定的路径的 exe 或 dll，其中包含提供程序的已本地化的消息资源，表示为 %dirid%\filename。

<a href="" id="parameterfile-path-to-file"></a>**ParameterFile**=*path-to-file*  
（可选） 指定 exe 或 dll，其中包含表示为 %dirid%\filename 的提供程序的参数字符串资源的路径。

<a href="" id="importchannel-channel-name"></a>**ImportChannel**=*channel-name*  
（可选） 指定已由另一个提供程序定义的通道。 有关详细信息，请参阅以下**指定的通道列表**部分。

<a href="" id="addchannel-channel-name-channel-type--channel-install-section-"></a>**AddChannel**=*channel-name*,*channel-type*\[,*channel-install-section*\]  
（可选） 指定一个通道具有子指令 （可选） 引用了一个 INF 编写器定义通道的安装-部分 INF 文件中的其他位置。 有关详细信息，请参阅以下**指定的通道列表**部分。

### <a name="specifying-a-channel-list"></a>指定通道列表

可以在提供程序指定的信道列表及其*事件提供程序安装部分*。 可以导入一个通道，也可以将通道添加到列表并保留这些通道的顺序。 有关详细信息，请参阅[定义通道](https://docs.microsoft.com/windows/desktop/WES/defining-channels)。

*通道名称*的提供程序使用的通道列表中必须唯一。 *通道名称*必须是少于 255 个字符，不能包含以下字符: >，<，&、"，|、\'，:，' '，'？ '，*，或与 ASCII 字符的值小于 31。

*通道类型*可以指定为以下数字值，可以用十进制表示之一，或如以下列表中，以十六进制表示法中所示。

<a href="" id="0x1--admin-"></a>**0x1** （管理员）  
管理员类型通道支持事件的目标最终用户、 管理员和技术支持人员。 写入到管理通道的事件应具有定义完善的解决方案，管理员可以在其进行操作。

<a href="" id="0x2--operational-"></a>**0x2** （操作）  
操作类型的通道支持用于分析和诊断问题或匹配项的事件。 可以使用它们来触发工具或基于问题或匹配项的任务。

<a href="" id="0x3--analytic-"></a>**0x3** （分析）  
Analytic 类型通道支持发布量非常大的事件。 它们描述程序操作，并指示无法处理的用户干预的问题。

<a href="" id="0x4--debug-"></a>**0x4** （调试）  
调试仅供开发人员用于诊断问题以进行调试的类型的通道支持事件。

**AddChannel**还可以引用子指令*通道安装部分*INF 文件中的其他位置。 每个此类部分具有以下形式：

```ini
[channel-install-section]

[Isolation=isolation-type]
[Access=access-string]
[Enabled=0|1]
[Value=value]
[LoggingMaxSize=max-size]
[LoggingRetention=retention-type]
[LoggingAutoBackup=0|1]
```

有关通道属性的详细信息，请参阅[ChannelType](https://docs.microsoft.com/windows/desktop/WES/eventmanifestschema-channeltype-complextype)中定义[EventManifest 架构](https://docs.microsoft.com/windows/desktop/WES/eventmanifestschema-schema)。

### <a name="channel-install-section-entries-and-values"></a>通道安装节条目和值

<a href="" id="isolation-isolation-type"></a>**隔离**=*隔离类型*  
（可选） 指定的信道的默认访问权限，作为以下数字值，可以用十进制表示之一，或者，如以下列表中，以十六进制表示法中所示。 如果省略，则此值默认为**0x1** （应用程序）。

<a href="" id="0x1--application-"></a>**0x1** （应用程序）  

<a href="" id="0x2--system-"></a>**0x2** （系统）  

<a href="" id="0x3--Custom-"></a>**0x3** （自定义）  

<a href="" id="access-access-string"></a>**Access**=*access-string*  
（可选） 指定[安全描述符定义语言](https://docs.microsoft.com/windows/desktop/SecAuthZ/security-descriptor-definition-language)(SDDL) 访问说明符控制访问到日志文件支持通道。

如果此字符串用于控制读取访问权限 （忽略的写入权限） 的文件**隔离**设置为**0x1** （应用程序） 或**0x2** （系统），同时可以控制通道和读取访问权限的文件，如果隔离属性设置为写入访问权限**0x3** （自定义）。

<a href="" id="enabled-0-1"></a>**已启用**=**0 | 1**  
（可选） 指定是否启用了通道。 如果省略，则默认为 0 （禁用）。

因为**0x3** （分析） 和**0x4** （调试）*通道类型*是大量通道应设置**已启用**为 1 时，才调查某个问题的一个组件，它将写入到该通道。 可以在每次**0x3** （分析） 和**0x4** （调试） 通道，该服务将清除从通道的事件。

<a href="" id="value-value"></a>**值**=*值*  
（可选） 指定唯一标识的提供程序定义的通道列表中的通道的数字标识符。

<a href="" id="loggingmaxsize-max-size"></a>**LoggingMaxSize**=*max-size*  
（可选） 指定的最大大小，以字节为单位的日志文件。 默认 （和最小值） 值为 1 MB。

<a href="" id="loggingretention-retention-type"></a>**LoggingRetention**=*retention-type*  
（可选） 指定日志文件是否处于**0x1** （循环） 或**0x2** （按顺序）。 默认值是**0x1** （循环） 对于**0x1** (Admin) 和**0x2** （操作）*通道类型*和**0x2**（按顺序） 的**0x3** （分析） 和**0x4** （调试）*通道类型*。

<a href="" id="loggingautobackup-0-1"></a>**LoggingAutoBackup**=**0|1**  
（可选） 指定是否创建新的日志文件，当当前日志文件达到其最大大小。 设置为 1，以请求该服务创建一个新文件，当日志文件达到其最大大小;否则为为 0。 可以设置**LoggingAutoBackup**到 1 才**LoggingRetention**设置为**0x2** （按顺序） 并且仅限于**0x1** (Admin) 和**0x2** （操作）*通道类型*。

<a name="examples"></a>示例
--------

此示例显示引用的事件提供程序安装各个部分**AddEventProvider**指令前面部分中的示例如前面所示[ * **DDInstall *。事件**](inf-ddinstall-events-section.md)。

```ini
[foo_Event_Provider_Inst]
ProviderName  = FooCollector
ResourceFile  = %13%\FooResource.dll
MessageFile   = %13%\FooMessage.exe

[bar_Event_Provider_Inst]
ProviderName  = BarCollector
ResourceFile  = %13%\BarResource.exe
MessageFile   = %13%\BarMessage.dll
ParameterFile = %13%\BarParameter.dll
ImportChannel = Microsoft-Windows-BaseProvider/Admin
AddChannel    = Bar-Provider/Admin,0x1,bar_Channel2_Inst    ; Admin type
ImportChannel = Microsoft-Windows-BaseProvider/Operational
ImportChannel = Microsoft-Windows-SampleProvider/Admin
AddChannel    = Bar-Provider/Debug,0x4                      ; Debug type

[bar_Channel2_Inst]
Isolation         = 2                                       ; System isolation
Enabled           = 1
Value             = 17
LoggingMaxSize    = 20971520
LoggingRetention  = 2                                       ; Sequential
LoggingAutoBackup = 1
```

## <a name="see-also"></a>请参阅


[***DDInstall *。事件**](inf-ddinstall-events-section.md)

 

 





