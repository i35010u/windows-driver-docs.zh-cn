---
title: INF DelService 指令
description: DelService 指令用于 DDInstall.Services 部分中，将删除其中一个或多个以前从目标计算机中安装驱动程序设备/服务。
ms.assetid: eca57f7c-1551-4247-ab1f-858e6e3ad9d7
keywords:
- INF DelService 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DelService Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7b0d1a47050af081d57ee2c9c6947bccbf49658
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567152"
---
# <a name="inf-delservice-directive"></a>INF DelService 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**DelService**中使用指令[ * **DDInstall *。服务**](inf-ddinstall-services-section.md)部分删除一个或多个以前从目标计算机安装设备/驱动程序服务。

```ini
[DDInstall.Services] 
 
DelService=ServiceName[,[flags][,[EventLogType][,EventName]]
...
```

## <a name="entries"></a>条目


<a href="" id="servicename"></a>*ServiceName*  
指定要删除的服务的名称。

对于设备，此值通常是其驱动程序，例如"sermouse，"有通用名称或一些此类名称。

<a href="" id="flags"></a>*flags*  
此可选值是指定一个或多个定义中的以下标志*Setupapi.h*，指定为十六进制值：

<a href="" id="0x00000004--spsvcinst-deleteeventlogentry-"></a>**0x00000004** (SPSVCINST_DELETEEVENTLOGENTRY)  
事件日志条目 （或项），它与给定 ServiceName 关联也应删除系统中。

<a href="" id="0x00000200---spsvcinst-stopservice--"></a>**0x00000200** (SPSVCINST_STOPSERVICE)   
删除前停止该服务。

<a href="" id="eventlogtype"></a>*EventLogType*  
（可选） 指定之一**系统**，**安全**，或**应用程序**。 如果要删除的事件日志的类型，可以省略这**系统**。

<a href="" id="eventname"></a>*EventName*  
（可选） 指定事件日志的名称。 如果它等同于指定可以省略这*ServiceName*条目。

<a name="remarks"></a>备注
-------

此指令很少使用。 可以安全地删除的唯一服务是操作系统的使用仅在早期版本，并因此永远不会使用当前安装的版本。

从 Windows XP，您可以使用*TargetOSVersion*修饰以控制特定于版本的安装行为。 有关此修饰的详细信息，请参阅[ **INF 制造商部分**](inf-manufacturer-section.md)。

但是，默认情况下提供的特定设备驱动程序的事件日志信息不从系统中删除在卸载，除非设备/驱动程序 INF 显式请求删除 (*标志*或*EventName*) 以及删除驱动程序服务的事件日志。

## <a name="see-also"></a>请参阅


[**AddService**](inf-addservice-directive.md)

[***DDInstall*.Services**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

 

 






