---
title: INF ClassInstall32.Services 节
description: ClassInstall32 部分的新类中的设备安装新的设备安装程序类 （和可能的类安装程序）。
ms.assetid: 602cf407-f3c0-4342-9e59-87481a0f41ef
keywords:
- INF ClassInstall32.Services 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF ClassInstall32.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a7b4a1e8c5978474b5121eac5626cea06b79d09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330916"
---
# <a name="inf-classinstall32services-section"></a>INF ClassInstall32.Services 节


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**ClassInstall32**部分中安装新[设备安装程序类](device-setup-classes.md)（和可能的类安装程序） 的新类中的设备。

```ini
[ClassInstall32.Services] | 
[ClassInstall32.nt.Services] | 
[ClassInstall32.ntx86.Services] | 
[ClassInstall32.ntarm.Services] | (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64.Services] | (Windows 10 version 1709 and later versions of Windows)
[ClassInstall32.ntia64.Services] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64.Services]  (Windows XP and later versions of Windows)

AddService=ServiceName,[flags],service-install-section
                             [,event-log-install-section[,[EventLogType][,EventName]]]...
[DelService=ServiceName[,[flags][,[EventLogType][,EventName]]]...]
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
```

每个**ClassInstall32.Services**一节包含一个或多个[ **INF AddService 指令**](inf-addservice-directive.md)引用 INF 文件中的其他 INF 编写器定义部分。

INF 文件通常使用**ClassInstall32.Services**上至少有一个部分**AddService**指令来控制如何以及何时加载特定设备类的服务，任何依赖项它可能会对其他服务，等等。 （可选） 他们还可以设置于设备类的事件日志记录服务。

## <a name="entries"></a>条目


<a href="" id="addservice-servicename--flags--service-install-section"></a>**AddService=**<em>ServiceName</em>,\[*flags*\]**,**<em>service-install-section</em>  

<a href="" id="----------------------------------------event-log-install-section---eventlogtype---eventname------"></a>                                      \[**,**<em>event-log-install-section</em>\[**,**\[*EventLogType*\]\[**,**<em>EventName</em>\]\]\]...  
此指令引用 INF 编写器定义服务的安装-部分和一个事件的日志-安装-部分覆盖的设备类的驱动程序的 INF 文件中的其他位置，也可能[ **ClassInstall32**](inf-classinstall32-section.md)部分。 有关详细信息，请参阅[ **INF AddService 指令**](inf-addservice-directive.md)。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**DelService=**<em>ServiceName</em>\[**,**\[*flags*\]\[**,**\[*EventLogType*\]\[**,**<em>EventName</em>\]\]\]...  
此指令从目标计算机中删除以前安装的服务。 很少使用此指令。 有关详细信息，请参阅[ **INF DelService 指令**](inf-delservice-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include=**<em>filename</em>**.inf**\[**,**<em>filename2</em>**.inf**\]...  
此可选项指定一个或多个其他系统提供命名的 INF 文件包含安装此设备类所需的部分。 如果指定此项时，通常那么**需要**条目。

有关详细信息**Include**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需要 =**<em>inf 部分名称</em>\[**，**<em>inf 部分名称</em>\]...  
此可选项指定特定的命名必须在此设备类的安装过程中处理的部分。 通常情况下，此类指定的部分是**ClassInstall32.Services**中列出系统提供 INF 文件中的节**Include**条目。 但是，它可以是任何部分此类中被引用**ClassInstall32.Services**部分。

**需要**条目不能嵌套。 (有关详细信息**需要**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md))。

<a name="remarks"></a>备注
-------

**ClassInstall32.Services**部分应具有其相关的相同平台和操作系统修饰[ **ClassInstall32 部分**](inf-classinstall32-section.md)。 例如， **ClassInstall32.ntx86**部分中将具有相应**ClassInstall32.ntx86.Services**部分。

不区分大小写 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，和 **.ntarm64**扩展插件可以将插入**ClassInstall32.Services**部分跨平台 INF 文件中的名称，如正式语法语句中所示。 有关详细信息，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

## <a name="see-also"></a>请参阅


[**ClassInstall32**](inf-classinstall32-section.md)

[**AddService**](inf-addservice-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。硬件**](inf-ddinstall-hw-section.md)

[**DelService**](inf-delservice-directive.md)

[***模型***](inf-models-section.md)

 

 






