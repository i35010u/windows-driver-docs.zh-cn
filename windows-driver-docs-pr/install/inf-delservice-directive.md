---
title: INF DelService 指令
description: 在 DDInstall 节中使用 DelService 指令从目标计算机中删除一个或多个以前安装的设备/驱动程序服务。
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
ms.openlocfilehash: f08b646b8ea08a0216817926f5b1ceadae5605a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813119"
---
# <a name="inf-delservice-directive"></a>INF DelService 指令


**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

在 DDInstall 中使用 **DelService** 指令 [**_DDInstall_。服务**](inf-ddinstall-services-section.md)部分，从目标计算机中删除一个或多个以前安装的设备/驱动程序服务。

```inf
[DDInstall.Services] 
 
DelService=ServiceName[,[flags][,[EventLogType][,EventName]]
...
```

## <a name="entries"></a>项


<a href="" id="servicename"></a>*ServiceName*  
指定要删除的服务的名称。

对于设备，此值通常是其驱动程序的通用名称，如 "sermouse" 或某些此类名称。

<a href="" id="flags"></a>*随意*  
此可选值为指定为十六进制值指定的以下一个或多个 *setupapi.log* 中定义的标志：

<a href="" id="0x00000004--spsvcinst-deleteeventlogentry-"></a>**0x00000004** (SPSVCINST_DELETEEVENTLOGENTRY)   
还应从系统中删除事件日志条目 (或与给定 ServiceName 关联) 条目。

<a href="" id="0x00000200---spsvcinst-stopservice--"></a>**0x00000200** (SPSVCINST_STOPSERVICE)    
在删除服务之前将其停止。

<a href="" id="eventlogtype"></a>*EventLogType*  
根据需要指定 **系统**、 **安全** 或 **应用程序** 之一。 如果要删除的事件日志的类型为 " **系统**"，则可以省略此事件日志。

<a href="" id="eventname"></a>*名*  
（可选）指定事件日志的名称。 如果它与指定的 *ServiceName* 条目相同，则可以省略此项。

<a name="remarks"></a>备注
-------

此指令很少使用。 只能安全删除的服务只是在早期版本的操作系统中使用的服务，因此永远不会用于当前安装的版本。

从 Windows XP 开始，你可以使用 *TargetOSVersion* 修饰来控制特定于版本的安装行为。 有关此效果的详细信息，请参阅 [**INF 制造商部分**](inf-manufacturer-section.md)。

但是，默认情况下，不会从卸载上的系统中删除特定设备驱动程序提供的事件日志信息，除非该设备/驱动程序的 INF 显式请求删除 (*标志* 或事件日志的事件 *名称*) ，同时删除驱动程序服务。

## <a name="see-also"></a>请参阅


[**AddService**](inf-addservice-directive.md)

[**_DDInstall_。服务器**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

 

 






