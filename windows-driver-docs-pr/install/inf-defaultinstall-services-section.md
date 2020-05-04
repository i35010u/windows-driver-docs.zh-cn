---
title: INF DefaultInstall.Services 节
description: DefaultInstall 节包含一个或多个 AddService 指令，这些指令引用 INF 文件中其他由 INF 编写器定义的部分。
ms.assetid: 2b066cf9-b6b7-42d0-b147-9b1849ff04db
keywords:
- INF DefaultInstall 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DefaultInstall.Services Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5c7622d2507bbb05551332ac7667d9afc360c4e
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223209"
---
# <a name="inf-defaultinstallservices-section"></a>INF DefaultInstall.Services 节


**注意**  如果您要构建通用或移动驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**DefaultInstall**节包含一个或多个[**AddService**](inf-addservice-directive.md)指令，这些指令引用 inf 文件中其他由 inf 编写器定义的部分。 本部分等效于[**INF *DDInstall*。服务**](inf-ddinstall-services-section.md)部分，用于与[**INF DefaultInstall**](inf-defaultinstall-section.md)部分关联。

```inf
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


<a href="" id="addservice-servicename--flags--service-install-section"></a>**AddService =**<em>ServiceName</em>**，**\[*标志*\]**，**<em>服务安装-部分</em>  

<a href="" id="-----------------------------------------------------------------------------------------event-log-install-section---eventlogtype---eventname------"></a>                                                   \[**，**\[<strong>,</strong>*EventLogType***,**\[\[<em>event-log-install-section</em>\]，事件日志中的 ...\]\]\]  
此指令在 INF 文件中*的其他位置*引用了一个由 inf 编写器定义的*服务安装部分*，也可能是在此[**DefaultInstall**](inf-defaultinstall-section.md)部分所涵盖的设备的驱动程序的 inf 文件中的其他地方。

有关详细信息，请参阅[**INF AddService 指令**](inf-addservice-directive.md)。

<a href="" id="delservice-servicename---flags----eventlogtype---eventname------"></a>**DelService =**<em>ServiceName</em>\[**，**\[*flags*\[*EventLogType***,**\]**,**<em>EventName</em>，EventLogType\]，事件名称 ...\]\]\[\]\[  
此指令从目标计算机中删除以前安装的服务。 此指令很少使用。

有关详细信息，请参阅[**INF DelService 指令**](inf-delservice-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**.inf**\[**，**<em>filename2</em>\]...**.inf**  
此可选条目指定一个或多个系统提供的其他 INF 文件，其中包含安装此设备所需的部分。 如果指定此项，则通常是**需要**输入。

有关其用法的**包含**项和限制的详细信息，请参阅[指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需求 =**<em>inf-名称</em>\[**，**<em>inf-节名称</em>\].。。  
此可选条目指定在安装此设备过程中必须处理的特定命名部分。 通常，此类命名部分是<em>DDInstall</em>**。**"**包含**项" 中列出的系统提供的 INF 文件中的 "服务" 部分。 但是，它可以是在此类<em>DDInstall</em>中引用的任何部分 **。服务**部分。

不能嵌套**需求**条目。 有关其用法的**需求**条目和限制的详细信息，请参阅[指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a name="remarks"></a>备注
-------

[**AddService**](inf-addservice-directive.md)指令控制加载特定驱动程序的服务的方式和时间、其他服务或它可能具有的基础（旧）驱动程序的依赖关系，等等。 此外，它还可以为驱动程序设置事件日志记录服务。

**请注意**  ，仅当 inf 文件也使用[**inf DefaultInstall**](inf-defaultinstall-section.md)部分时，才使用**DefaultInstall**部分。 否则，它们使用[**INF *DDInstall*。服务**](inf-ddinstall-services-section.md)部分和[**INF *DDInstall* **](inf-ddinstall-section.md)部分。

 

**DefaultInstall**节应与它们相关的**DefaultInstall**部分具有相同的平台和操作系统修饰。 例如， **DefaultInstall. ntx86**部分会有一个对应的**DefaultInstall. ntx86**节。 有关如何使用**系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm**和**Ntarm64**扩展的详细信息，请参阅[为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<a name="examples"></a>示例
--------

请参阅为[**INF *DDInstall*提供的示例。服务**](inf-ddinstall-services-section.md)部分。

## <a name="see-also"></a>另请参阅


[***DDInstall***](inf-ddinstall-section.md)

[**DefaultInstall**](inf-defaultinstall-section.md)

 

 






