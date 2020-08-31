---
title: INF ClassInstall32.Services 节
description: ClassInstall32 节 (安装新的设备安装程序类，并为新类中的设备安装类安装程序) 。
ms.assetid: 602cf407-f3c0-4342-9e59-87481a0f41ef
keywords:
- INF ClassInstall32 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF ClassInstall32.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0132f6d7205d25a02ced8fe91550b38a0a1db2dc
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096427"
---
# <a name="inf-classinstall32services-section"></a>INF ClassInstall32.Services 节


**注意**   如果要构建通用或移动驱动程序包，此部分无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**ClassInstall32**节 (安装新的[设备安装程序类](./overview-of-device-setup-classes.md)，并可能为新类中的设备安装类安装程序) 。

```inf
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

每个 **ClassInstall32** 部分都包含一个或多个 [**inf AddService 指令**](inf-addservice-directive.md) ，这些指令引用 inf 文件中其他由 inf 编写器定义的部分。

INF 文件通常使用 **ClassInstall32** 部分和至少一个 **AddService** 指令来控制如何以及何时加载特定设备类的服务、它可能对其他服务产生的任何依赖关系等。 另外，他们还可以为设备类设置事件日志记录服务。

## <a name="entries"></a>项


<a href="" id="addservice-servicename--flags--service-install-section"></a>**AddService =**<em>ServiceName</em>， \[ *标志* \] **，**<em>服务安装-部分</em>  

<a href="" id="----------------------------------------event-log-install-section---eventlogtype---eventname------"></a>                                      \[**，**<em>event-log-install-section</em> \[ **,** \[ *EventLogType* \] \[ **,**<em>EventName</em> \] ， \] \] 事件日志中的 .。。  
此指令在 INF 文件中的其他位置引用一个由 INF 编写器定义的服务安装节，还可能在 [**ClassInstall32**](inf-classinstall32-section.md) 节涵盖的设备类的驱动程序的驱动程序中提供。 有关详细信息，请参阅 [**INF AddService 指令**](inf-addservice-directive.md)。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**DelService =**<em>ServiceName</em> \[ **，** \[ *flags* \] \[ **，** \[ *EventLogType* \] \[ **，**<em>事件名称</em> \] \] \] .。。  
此指令从目标计算机中删除以前安装的服务。 此指令很少使用。 有关详细信息，请参阅 [**INF DelService 指令**](inf-delservice-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**.inf** \[ **，**<em>filename2</em>**.inf** \] .。。  
此可选条目指定一个或多个其他系统提供的命名 INF 文件，其中包含安装此设备类所需的部分。 如果指定此项，则通常是 **需要** 输入。

有关其用法的 **包含** 项和限制的详细信息，请参阅 [指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需求 =**<em>inf-名称</em> \[ **，**<em>inf-节名称</em> \] .。。  
此可选条目指定在安装此设备类的过程中必须处理的特定命名部分。 通常，此类命名部分是系统提供的 INF 文件中的 **ClassInstall32** 部分，该文件在 **包含** 项中列出。 但是，它可以是在此类 **ClassInstall32** 部分中引用的任何部分。

不能嵌套**需求**条目。  (有关其使用 **情况的详细** 信息，请参阅 [指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)) 。

<a name="remarks"></a>备注
-------

**ClassInstall32** 节应与它们相关的 [**ClassInstall32 部分**](inf-classinstall32-section.md)具有相同的平台和操作系统修饰。 例如， **ClassInstall32. ntx86** 部分会有一个对应的 **ClassInstall32. ntx86** 节。

不 **区分大小**写的 **ntx86、.** **ntia64**、 **. ntamd64**、 **NTARM**和 **Ntarm64** 扩展可以插入到跨平台 INF 文件中的 **ClassInstall32** 节名称中，如正式语法语句中所示。 有关详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

## <a name="see-also"></a>另请参阅


[**ClassInstall32**](inf-classinstall32-section.md)

[**AddService**](inf-addservice-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.HW**](inf-ddinstall-hw-section.md)

[**DelService**](inf-delservice-directive.md)

[***模型***](inf-models-section.md)

 

