---
title: INF DDInstall.Events 节
description: 每个模型的 DDInstall 节都包含一个或多个 INF AddEventProvider 指令，这些指令引用 INF 文件中其他由 INF 编写器定义的部分。
keywords:
- INF DDInstall 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.Events Section
api_type:
- NA
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: a12f0196b244678e3e6c79156f12bf413764fdcc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790569"
---
# <a name="inf-ddinstallevents-section"></a>INF DDInstall.Events 节

每个模型 <em>DDInstall</em>**。Events** 节包含一个或多个 [**inf AddEventProvider 指令**](inf-addeventprovider-directive.md) ，这些指令引用 inf 文件中其他由 inf 编写器定义的部分。 Windows 10 版本1809及更高版本支持此部分。

```inf
[install-section-name.Events] |
[install-section-name.nt.Events] |
[install-section-name.ntx86.Events] |
[install-section-name.ntia64.Events] |
[install-section-name.ntamd64.Events] |
[install-section-name.ntarm.Events] |
[install-section-name.ntarm64.Events] |

AddEventProvider={ProviderGUID},event-provider-install-section
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...] 
```

可以提供 <em>DDInstall</em>**。** 包含至少一个 **AddEventProvider** 指令的 Events 节，用于为 Windows (ETW) 提供程序注册 [事件跟踪](/windows/desktop/ETW/about-event-tracing) 。

## <a name="entries"></a>项

<a href="" id="addeventprovider--providerguid--event-provider-install-section"></a>**AddEventProvider =**{*ProviderGUID*}，*事件提供程序-安装部分*  
此指令在 INF 文件中的其他位置引用由 INF 编写器定义的 DDInstall *节*，其中包含此 *DDInstall* 部分涵盖的设备的驱动程序。 有关详细信息，请参阅 [**INF AddEventProvider 指令**](inf-addeventprovider-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**.inf** \[ **，**<em>filename2</em>**.inf** \] .。。  
此可选条目指定一个或多个系统提供的其他 INF 文件，其中包含安装此设备所需的部分。 如果指定此项 **，则通常还需要输入。**

有关其用法的 **包含** 项和限制的详细信息，请参阅 [指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需求 =**<em>inf-名称</em> \[ **，**<em>inf-节名称</em> \] .。。  
此可选条目指定在安装此设备过程中必须处理的部分。 通常，部分是 <em>DDInstall</em>**。****包含在包含** 项中的系统提供的 INF 文件中的事件部分。 但是，它可以是在 DDInstall 中引用的任何节 <em>DDInstall</em>**。事件** 部分。

不能嵌套 **需求** 条目。 有关其用法的 **需求** 条目和限制的详细信息，请参阅 [指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a name="remarks"></a>备注
-------

<em>DDInstall</em>**。事件** 部分应该与它们相关的 [ * *_DDInstall_* _](inf-ddinstall-section.md)部分具有相同的平台和操作系统修饰。 例如，<em>安装节名称</em>*ntx86** 节会有相应的 <em>安装节名称</em>**. ntx86。事件** 部分。

在 INF 文件的 "每制造商"*型号* 部分下，必须在特定于设备/模型的条目中引用指定的 *DDInstall* 部分。 在正式语法语句中显示的 *安装节名称* 不区分大小写的扩展可以插入到此类 <em>DDInstall</em>中 **。** 跨平台 INF 文件中的事件部分名称。

有关如何使用 **系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm** 和 **Ntarm64** 扩展的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<a name="examples"></a>示例
--------

此示例显示了 <em>安装部分的名称</em>**。** INF 文件中的事件部分及其事件提供程序安装部分。

```inf
[Device_Inst.NT.Events]
AddEventProvider={071acb53-ccfb-42e0-9a68-5336b7301507},foo_Event_Provider_Inst
AddEventProvider={6d3fd9ef-bcbb-42d7-9fbd-1bf2d926b394},bar_Event_Provider_Inst

; entries in the following xxx_Inst sections omitted here for brevity,
; but fully specified as the example for the AddEventProvider directive
;
[foo_Event_Provider_Inst]
; ...

[bar_Event_Provider_Inst]
; ...
```

## <a name="see-also"></a>请参阅


[**AddEventProvider**](inf-addeventprovider-directive.md)

[**_DDInstall_**](inf-ddinstall-section.md)

 

