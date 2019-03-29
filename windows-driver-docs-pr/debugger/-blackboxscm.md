---
title: blackboxscm
description: Blackboxscmextension 显示服务控制管理器 (scm) 第二个启动数据。
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
ms.openlocfilehash: ccd8d70b2c02a57c6a280fa0bd7c61cb406cfc83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576109"
---
# <a name="blackboxscm"></a>!blackboxscm

**！ Blackboxscm**扩展可用时在内核模式转储文件中显示信息从服务控制管理器 (SCM)。 该扩展将显示具有未完成的服务控制请求的任何服务的名称。    从内核模式转储时检测的错误发生，以及可能始终无法保存中缓存的数据检索的信息。


语法

```dbgcmd
!blackboxscm  
```

## <a name="span-idparametersspanparameters"></a><span id="Parameters"></span>参数

*无*   


## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ext.dll


## <a name="span-idremarksspanremarks"></a><span id="Remarks"></span>备注

命令调度到的特定服务的 LPHANDLER_FUNCTION_EX 回调函数。  
如有序地关闭或重新启动计算机，可以延迟 SERVICE_CONTROL_SHUTDOWN 或 SERVICE_CONTROL_PRESHUTDOWN，请求数。

### <a name="example-command-output"></a>示例命令输出 

在多个转储文件，将返回单个服务。

```dbgcmd
2: kd> !ext.blackboxscm
    Name: gpsvc
    Code: 15
```

返回的数据提供有关两个字段的信息。

*名称*-在转储发生时处于活动状态的服务的名称。

*代码*-dwControl 这是未完成的十进制值

在此示例中，代码 15 （或 0x0000000F） 被指 SERVICE_CONTROL_PRESHUTDOWN。


### <a name="multiple-services"></a>多个服务

列出了多个服务，只列出的第一个服务时通常要进行失败分析感兴趣。  这是因为 SCM （服务控制管理器） 等待按顺序完成这些请求，因此，只有第一个服务实际接收到控制请求。

有关 SCM 详细信息，请参阅[服务控制管理器](https://docs.microsoft.com/en-us/windows/desktop/Services/service-control-manager)。


### <a name="span-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span>其他信息

定义在 winsvc.h dwControl 值并将其记录为参数[LPHANDLER_FUNCTION_EX 回调函数](https://docs.microsoft.com/windows/desktop/api/winsvc/nc-winsvc-lphandler_function_ex#parameters)。

 


