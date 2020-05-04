---
title: INF DelService 指令
description: 在 DDInstall 节中使用 DelService 指令从目标计算机中删除一个或多个以前安装的设备/驱动程序服务。
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
ms.openlocfilehash: 8f64f6ed464c29e6977965d0254399851d316c74
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223179"
---
# <a name="inf-delservice-directive"></a>INF DelService 指令


**注意：**  如果要生成通用或移动驱动程序包，则此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

DDInstall * 中使用了**DelService**指令。 [ *服务](inf-ddinstall-services-section.md)部分，从目标计算机中删除一个或多个以前安装的设备/驱动程序服务。

```inf
[DDInstall.Services] 
 
DelService=ServiceName[,[flags][,[EventLogType][,EventName]]
...
```

## <a name="entries"></a>条目


<a href="" id="servicename"></a>*ServiceName*  
指定要删除的服务的名称。

对于设备，此值通常是其驱动程序的通用名称，如 "sermouse" 或某些此类名称。

<a href="" id="flags"></a>*随意*  
此可选值为指定为十六进制值指定的以下一个或多个*setupapi.log*中定义的标志：

<a href="" id="0x00000004--spsvcinst-deleteeventlogentry-"></a>**0x00000004** （SPSVCINST_DELETEEVENTLOGENTRY）  
还应从系统中删除与给定 ServiceName 关联的事件日志条目（或条目）。

<a href="" id="0x00000200---spsvcinst-stopservice--"></a>**0x00000200** （SPSVCINST_STOPSERVICE）   
在删除服务之前将其停止。

<a href="" id="eventlogtype"></a>*EventLogType*  
根据需要指定**系统**、**安全**或**应用程序**之一。 如果要删除的事件日志的类型为 "**系统**"，则可以省略此事件日志。

<a href="" id="eventname"></a>*名*  
（可选）指定事件日志的名称。 如果它与指定的*ServiceName*条目相同，则可以省略此项。

<a name="remarks"></a>备注
-------

此指令很少使用。 只能安全删除的服务只是在早期版本的操作系统中使用的服务，因此永远不会用于当前安装的版本。

从 Windows XP 开始，你可以使用*TargetOSVersion*修饰来控制特定于版本的安装行为。 有关此效果的详细信息，请参阅[**INF 制造商部分**](inf-manufacturer-section.md)。

但是，默认情况下，不会从卸载上的系统中删除特定设备驱动程序提供的事件日志信息，除非设备/驱动程序的 INF 显式请求了事件日志的删除（*标志*或*事件名称*）以及删除驱动程序服务。

## <a name="see-also"></a>另请参阅


[**AddService**](inf-addservice-directive.md)

[***DDInstall*.服务器**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

 

 






