---
title: blackboxscm
description: Blackboxscmextension 显示服务控制管理器 (scm) 辅助启动数据。
keywords:
- blackboxscm Windows 调试
ms.author: windowsdriverdev
ms.date: 01/02/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- blackboxscm
api_type:
- NA
ms.openlocfilehash: f6fc46c6449a80b5a0ef9d24664a29e6816af5cd
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716976"
---
# <a name="blackboxscm"></a>!blackboxscm

当 **blackboxscm** 扩展在内核模式转储文件中可用时，它会显示服务控制管理器 (SCM) 的信息。 该扩展将显示具有未完成的服务控制请求的任何服务的名称。    从内核模式转储中的缓存数据中检索信息，该转储是在检测到错误时保存的，并且可能并非始终可用。


语法

```dbgcmd
!blackboxscm  
```

## <a name="span-idparametersspanparameters"></a><span id="Parameters"></span>参数

*无*   


## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

ext.dll


## <a name="span-idremarksspanremarks"></a><span id="Remarks"></span>注释

命令已分派给特定服务的 LPHANDLER_FUNCTION_EX 回调函数。  
未完成的请求（如 SERVICE_CONTROL_SHUTDOWN 或 SERVICE_CONTROL_PRESHUTDOWN）可能会延迟计算机的有序关闭或重新启动。

### <a name="example-command-output"></a>示例命令输出 

在许多转储文件中，只返回一个服务。

```dbgcmd
2: kd> !ext.blackboxscm
    Name: gpsvc
    Code: 15
```

返回的数据提供两个字段的相关信息。

*名称* -发生转储时处于活动状态的服务的名称。

*Code* -未完成的 DwControl 的十进制值

在此示例中，代码 15 (或 0x0000000F) 定义为 SERVICE_CONTROL_PRESHUTDOWN。


### <a name="multiple-services"></a>多个服务

如果列出了多个服务，则只有列出的第一项服务通常对失败分析感兴趣。  这是因为 SCM (服务控制管理器) 按顺序等待这些请求的完成，因此只有第一个服务实际接收了控制请求。

有关 SCM 的详细信息，请参阅 [服务控制管理器](/windows/desktop/Services/service-control-manager)。


### <a name="span-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span>附加信息

dwControl 值在 winsvc 中定义，并记录为 [LPHANDLER_FUNCTION_EX 回调函数](/windows/win32/api/winsvc/nc-winsvc-lphandler_function_ex#parameters)的参数。

 