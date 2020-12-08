---
title: INF AddEventProvider 指令
description: AddEventProvider 指令用于 INF DDInstall 部分中。
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
ms.openlocfilehash: 60469435c247c6766d28a6c9cd6faab3458a9388
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840065"
---
# <a name="inf-addeventprovider-directive"></a>INF AddEventProvider 指令

在 INF DDInstall 中使用 **AddEventProvider** 指令 [**。 *DDInstall* 事件部分**](inf-ddinstall-services-section.md)。 它指定与驱动程序相关联的 Windows (ETW) 提供程序的 [事件跟踪](/windows/desktop/ETW/about-event-tracing) 特性。 Windows 10 版本1809及更高版本支持此指令。

```inf
[DDInstall.Events] 

AddEventProvider={ProviderGUID},event-provider-install-section
...
```

## <a name="entries"></a>项


<a href="" id="ProviderGUID"></a>*ProviderGUID*  
指定标识提供程序的 GUID 值。 这可以表示为形式的显式 GUID 值，或表示为 `{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}` `{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}` INF 文件的 [**字符串**](inf-strings-section.md) 部分中定义的% strkey% 令牌。

<a href="" id="event-provider-install-section"></a>*事件提供程序-安装-部分*  
引用由 INF 写入方定义的部分，其中包含为此设备 (或设备) 注册提供程序的信息。 有关详细信息，请参阅下面的 " **备注** " 部分。

<a name="remarks"></a>备注
-------

系统定义和不区分大小写的扩展可以插入 <em>DDInstall</em>**。事件** 部分，其中包含跨操作系统系统和/或跨平台 INF 文件中的 **AddEventProvider** 指令，用于指定特定于平台或特定于操作系统的安装。

在 INF 文件中，每个 INF 编写器创建的节名称必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

**AddEventProvider** 指令必须在 INF 文件中的其他位置引用已命名的 *事件提供程序安装部分*。 每个此类部分都具有以下形式：

```inf
[event-provider-install-section]
 
ProviderName=name
ResourceFile=path-to-file
[MessageFile=path-to-file]
[ParameterFile=path-to-file]
(ImportChannel=channel-name) |
(AddChannel=channel-name,channel-type[,channel-install-section])
...
```

每个 *事件提供程序安装部分* 必须提供 **ProviderName** 和 **ResourceFile**。 （可选）使用 **ImportChannel (s)** 和 **AddChannel (s)** 的任意组合指定提供程序的通道列表，每个通道在单独的行上。 有关 INF 文件中的通道列表的详细信息，请参阅下面 [**的指定通道列表**](#specifying-a-channel-list) 。 有关 [Windows 事件日志](/windows/desktop/WES/windows-event-log) 通道的详细信息，请参阅 [定义通道](/windows/desktop/WES/defining-channels)。

### <a name="event-provider-install-section-entries-and-values"></a>事件提供程序-安装节项和值

<a href="" id="providername-name"></a>**ProviderName** =*名称*  
指定提供程序的名称。 名称长度不能超过255个字符，并且不能包含以下字符： ">"、"<"、"&"、"" "、" | "、" " \' 、"： "、" ""、"？"、"*" 或 ASCII 值小于31的字符。 此外，此名称必须遵循有关文件和注册表项名称的一般约束。 可在 [命名文件](/windows/desktop/FileIO/naming-a-file) 和 [注册表元素大小限制](/windows/desktop/SysInfo/registry-element-size-limits)中找到这些约束。

<a href="" id="resourcefile-path-to-file"></a>**ResourceFile** =*路径到文件*  
指定包含提供程序的元数据资源的 exe 或 dll 的路径，表示为%dirid%\filename。

*Dirid* 号可以是自定义目录标识符，也可以是 [使用 Dirids](using-dirids.md)中所述的系统定义的目录标识符之一。

<a href="" id="messagefile-path-to-file"></a>**MessageFile** =*路径到文件*  
（可选）指定包含提供程序的本地化消息资源（以%dirid%\filename. 表示）的 exe 或 dll 的路径。

<a href="" id="parameterfile-path-to-file"></a>**ParameterFile** =*路径到文件*  
（可选）指定包含提供程序的参数字符串资源的 exe 或 dll 的路径，表示为%dirid%\filename。

<a href="" id="importchannel-channel-name"></a>**ImportChannel** =*通道名称*  
根据需要，还可以指定已由另一个提供程序定义的通道。 有关详细信息，请参阅以下 **指定频道列表** 部分。

<a href="" id="addchannel-channel-name-channel-type--channel-install-section-"></a>**AddChannel** =*通道名称*，*通道类型* \[ ，*通道安装-部分*\]  
（可选）使用子指令指定一个通道，该子指令可以选择引用 INF 文件中其他位置的 INF 写入器定义的通道安装部分。 有关详细信息，请参阅以下 **指定频道列表** 部分。

### <a name="specifying-a-channel-list"></a>指定频道列表

可以在其 *事件提供程序-安装部分* 中为提供程序指定通道列表。 你可以导入通道或向列表中添加频道，并保留这些通道的顺序。 有关详细信息，请参阅 [定义通道](/windows/desktop/WES/defining-channels)。

*信道名称* 在提供程序使用的通道列表中必须是唯一的。 *通道名称* 必须少于255个字符，并且不能包含以下字符： ">"、"<"、"&"、"" "、" | "、" " \' 、"： "、" ""、"？"、"*" 或 ASCII 值小于31的字符。

*通道类型* 可以指定为以下数字值之一，以十进制或形式表示，如下面的列表所示，采用十六进制表示法。

<a href="" id="0x1--admin-"></a>**0x1** (管理员)   
管理类型通道支持面向最终用户、管理员和支持人员的事件。 写入管理通道的事件应该有一个明确定义的解决方案，管理员可以在该解决方案中执行操作。

<a href="" id="0x2--operational-"></a>**0x2** (操作)   
操作类型通道支持用于分析和诊断问题的事件。 它们可用于根据问题或发生的事件触发工具或任务。

<a href="" id="0x3--analytic-"></a>**0x3** (分析)   
分析类型通道支持大容量发布的事件。 它们描述程序操作并指示用户无法处理的问题。

<a href="" id="0x4--debug-"></a>**0x4** (调试)   
调试类型通道支持仅由开发人员用来诊断问题以进行调试的事件。

**AddChannel** 子指令还可在 INF 文件中的其他位置引用 *通道安装部分*。 每个此类部分都具有以下形式：

```inf
[channel-install-section]

[Isolation=isolation-type]
[Access=access-string]
[Enabled=0|1]
[Value=value]
[LoggingMaxSize=max-size]
[LoggingRetention=retention-type]
[LoggingAutoBackup=0|1]
```

有关通道属性的详细信息，请参阅在[EventManifest 架构](/windows/desktop/WES/eventmanifestschema-schema)中定义的[ChannelType](/windows/desktop/WES/eventmanifestschema-channeltype-complextype) 。

### <a name="channel-install-section-entries-and-values"></a>Channel-Install 节项和值

<a href="" id="isolation-isolation-type"></a>**隔离** =*隔离类型*  
（可选）将通道的默认访问权限指定为以下其中一个数值（用 decimal 或表示），如下面的列表所示，用十六进制表示法表示。 如果省略，则默认为 **0x1** (应用程序) 。

<a href="" id="0x1--application-"></a>**0x1** (应用程序)   

<a href="" id="0x2--system-"></a>**0x2** (系统)   

<a href="" id="0x3--Custom-"></a>**0x3** (自定义)   

<a href="" id="access-access-string"></a>**访问** =*访问字符串*  
根据需要，还可以指定 [安全描述符定义语言](/windows/desktop/SecAuthZ/security-descriptor-definition-language) (SDDL) 访问描述符，控制对支持通道的日志文件的访问。

此字符串控制对文件的读取访问权限，)  (如果 **隔离** 设置为 **0X1** (应用程序) 或 **0x2** (系统) ，则它控制通道的写入访问权限，并在隔离特性设置为 **0x3** (自定义) 时，控制对文件的读取访问权限。

<a href="" id="enabled-0-1"></a>**已启用** =**0 | 1**  
根据需要指定是否启用通道。 如果省略，则默认为 0 (禁用) 。

因为 **0x3** (分析) 和 **0x4** (调试) *通道类型* 为大容量通道，所以仅当调查写入到该通道的组件的问题时，才应将 **Enabled** 设置为1。 每次启用 **0x3** (分析) 和 **0x4** (调试) 通道时，服务将从通道中清除事件。

<a href="" id="value-value"></a>**值** =*值*  
（可选）指定一个数字标识符，该标识符唯一标识提供程序所定义的通道列表中的通道。

<a href="" id="loggingmaxsize-max-size"></a>**LoggingMaxSize** =*最大大小*  
根据需要指定日志文件的最大大小（以字节为单位）。 默认 (和最小) 值为 1 MB。

<a href="" id="loggingretention-retention-type"></a>**LoggingRetention** =*保留类型*  
根据需要指定日志文件是否为 **0x1** (循环) 或 **0x2** (顺序) 。 默认情况下 **，0x1 (为** 0x1) ，为 **0x1** (Admin) 和 **0x2** (*操作)  () 分析* (和 **0x4** **)  ()** **的顺序** *。*

<a href="" id="loggingautobackup-0-1"></a>**LoggingAutoBackup** =**0 | 1**  
根据需要指定在当前日志文件达到其最大大小时是否创建新的日志文件。 设置为1，请求服务在日志文件达到其最大大小时创建新文件;否则为0。 仅当 **LoggingRetention** 设置为 **0x2** (顺序) 并且只有 **0x1** (Admin) 和 **0x2** (操作) *通道类型* 时，才能将 **LoggingAutoBackup** 设置为1。

<a name="examples"></a>示例
--------

此示例显示了 **AddEventProvider** 指令所引用的事件提供程序安装部分，如 DDInstall 的示例中所示 [**_DDInstall_。事件**](inf-ddinstall-events-section.md)。

```inf
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


[**_DDInstall_。事件**](inf-ddinstall-events-section.md)

 

