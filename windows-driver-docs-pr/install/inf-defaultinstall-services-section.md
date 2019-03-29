---
title: INF DefaultInstall.Services 节
description: DefaultInstall.Services 部分包含一个或多个 AddService 指令引用的 INF 文件中的其他 INF 编写器定义部分。
ms.assetid: 2b066cf9-b6b7-42d0-b147-9b1849ff04db
keywords:
- INF DefaultInstall.Services 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DefaultInstall.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8be52df2e4c63809585269c414a6f720e7853359
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563918"
---
# <a name="inf-defaultinstallservices-section"></a>INF DefaultInstall.Services 节


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**DefaultInstall.Services**一节包含一个或多个[ **AddService** ](inf-addservice-directive.md)指令引用的 INF 文件中的其他 INF 编写器定义部分。 本部分是等效于[ **INF *DDInstall*。服务**](inf-ddinstall-services-section.md)部分，并使用与建立关联[ **INF DefaultInstall** ](inf-defaultinstall-section.md)部分。

```ini
[DefaultInstall.Services] |
[DefaultInstall.nt.Services] |
[DefaultInstall.ntx86.Services] |
[DefaultInstall.ntarm.Services] | (Windows 8 and later versions of Windows)
[DefaultInstall.ntarm64.Services]  (Windows 10 version 1709 and later versions of Windows)
[DefaultInstall.ntia64.Services] | (Windows XP and later versions of Windows)
[DefaultInstall.ntamd64.Services]  (Windows XP and later versions of Windows)
 
AddService=ServiceName,[flags],service-install-section
                             [,event-log-install-section[,[EventLogType][,EventName]]]...]
[DelService=ServiceName[,[flags][,[EventLogType][,EventName]]]...]
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
```

## <a name="entries"></a>条目


<a href="" id="addservice-servicename--flags--service-install-section"></a>**AddService=**<em>ServiceName</em>**,**\[*flags*\]**,**<em>service-install-section</em>  

<a href="" id="-----------------------------------------------------------------------------------------event-log-install-section---eventlogtype---eventname------"></a>                                                   \[**,**<em>event-log-install-section</em>\[**,**\[*EventLogType*\]\[<strong>,</strong>EventName\]\]\]...  
此指令引用 INF 编写器的定义*服务安装部分*，并且可能*事件日志-安装部分*其他位置中 INF 文件的设备驱动程序涵盖此[**DefaultInstall** ](inf-defaultinstall-section.md)部分。

有关详细信息，请参阅[ **INF AddService 指令**](inf-addservice-directive.md)。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**DelService=**<em>ServiceName</em>\[**,**\[*flags*\]\[**,**\[*EventLogType*\]\[**,**<em>EventName</em>\]\]\]...  
此指令从目标计算机中删除以前安装的服务。 很少使用此指令。

有关详细信息，请参阅[ **INF DelService 指令**](inf-delservice-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include=**<em>filename</em>**.inf**\[**,**<em>filename2</em>**.inf**\]...  
此可选项指定一个或多个其他系统提供 INF 文件包含安装此设备所需的部分。 如果指定此项时，通常那么**需要**条目。

有关详细信息**Include**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需要 =**<em>inf 部分名称</em>\[**，**<em>inf 部分名称</em>\]...  
此可选项指定特定的命名必须在此设备的安装过程中处理的部分。 通常情况下，此类指定的部分是<em>DDInstall</em>**。服务**中列出系统提供 INF 文件中的节**Include**条目。 但是，它可以是任何部分此类中被引用<em>DDInstall</em>**。服务**部分。

**需要**条目不能嵌套。 有关详细信息**需要**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a name="remarks"></a>备注
-------

[ **AddService** ](inf-addservice-directive.md)指令都可以控制如何以及何时的特定驱动程序的服务已加载，它可能会有，和等等的基础 （旧版） 驱动程序或其他服务上的任何依赖项。 （可选），它可以设置的驱动程序的事件日志记录服务。

**请注意**  INF 文件使用**DefaultInstall.Services**部分仅当他们还可以使用[ **INF DefaultInstall** ](inf-defaultinstall-section.md)部分。 否则，它们使用[ **INF *DDInstall*。服务**](inf-ddinstall-services-section.md)一起使用部分[ **INF *DDInstall***  ](inf-ddinstall-section.md)部分。

 

**DefaultInstall.Services**部分应具有其相关的相同平台和操作系统修饰**DefaultInstall**部分。 例如， **DefaultInstall.ntx86**部分中将具有相应**DefaultInstall.ntx86.Services**部分。 有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<a name="examples"></a>示例
--------

请参阅为提供的示例[ **INF *DDInstall*。服务**](inf-ddinstall-services-section.md)部分。

## <a name="see-also"></a>请参阅


[***DDInstall***](inf-ddinstall-section.md)

[**DefaultInstall**](inf-defaultinstall-section.md)

 

 






