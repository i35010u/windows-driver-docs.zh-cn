---
title: INF DDInstall.Events 节
author: andylsn
description: 每个每个模型 DDInstall.Events 部分包含一个或多个引用的 INF 文件中的其他 INF 编写器定义部分的 INF AddEventProvider 指令。
ms.assetid: ''
keywords:
- INF DDInstall.Events 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.Events Section
api_type:
- NA
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8f46a416ceb244e5532115b9666e4586899f3c41
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341489"
---
# <a name="inf-ddinstallevents-section"></a>INF DDInstall.Events 节

每个每个模型<em>DDInstall</em>**。事件**部分包含一个或多个[ **INF AddEventProvider 指令**](inf-addeventprovider-directive.md)引用 INF 文件中的其他 INF 编写器定义部分。 本部分适用于 Windows 10 版本 1809年及更高版本。

```ini
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

你可以提供<em>DDInstall</em>**。事件**上至少有一个部分**AddEventProvider**指令来注册[Windows 的事件跟踪](https://msdn.microsoft.com/library/windows/desktop/aa363668)(ETW) 提供程序。

## <a name="entries"></a>条目

<a href="" id="addeventprovider--providerguid--event-provider-install-section"></a>**AddEventProvider=**{*ProviderGUID*},*event-provider-install-section*  
此指令引用 INF 编写器的定义*事件提供程序安装部分*涵盖此设备的驱动程序的 INF 文件中的其他位置*DDInstall*部分。 有关详细信息，请参阅[ **INF AddEventProvider 指令**](inf-addeventprovider-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include=**<em>filename</em>**.inf**\[**,**<em>filename2</em>**.inf**\]...  
此可选项指定一个或多个其他系统提供 INF 文件包含安装此设备所需的部分。 如果指定此项，则**需要**输入也是通常所需。

有关详细信息**Include**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需要 =**<em>inf 部分名称</em>\[**，**<em>inf 部分名称</em>\]...  
此可选项指定必须在此设备的安装过程中处理的部分。 通常情况下，部分是<em>DDInstall</em>**。事件**中列出系统提供 INF 文件中的节**Include**条目。 但是，它可以是任何部分中引用的<em>DDInstall</em>**。事件**部分。

**需要**条目不能嵌套。 有关详细信息**需要**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a name="remarks"></a>备注
-------

<em>DDInstall</em>**。事件**部分应具有其相关的相同平台和操作系统修饰[ ***DDInstall*** ](inf-ddinstall-section.md)部分。 例如，<em>安装的部分名称</em>**.ntx86**部分中将具有相应<em>安装部分名称</em>**.ntx86。事件**部分。

指定*DDInstall*部分必须在每个制造商下的特定于设备/模型的项中引用*模型*INF 文件部分。 不区分大小写的扩展*安装的部分名称*所示在正式语法语句可插入到此类<em>DDInstall</em>**。事件**跨平台 INF 文件中的节名称。

有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<a name="examples"></a>示例
--------

此示例演示<em>安装的部分名称</em>**。事件**部分和其事件的提供程序的安装-部分 INF 文件中。

```ini
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

[***DDInstall***](inf-ddinstall-section.md)

 

 





