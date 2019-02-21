---
title: OID_CO_TAPI_GET_CALL_DIAGNOSTICS
description: 本主题介绍 OID_CO_TAPI_GET_CALL_DIAGNOSTICS 对象标识符 (OID)。
ms.assetid: 5b0b1a96-9d66-4ee3-9b9a-3341ca3a4b5c
keywords:
- OID_CO_TAPI_GET_CALL_DIAGNOSTICS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3bd7effbbe9fc5f1b5bff2da30037b8fec31954
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520604"
---
# <a name="oidcotapigetcalldiagnostics"></a>OID_CO_TAPI_GET_CALL_DIAGNOSTICS

OID_CO_TAPI_GET_CALL_DIAGNOSTICS OID 请求呼叫管理器或 MCM 驱动程序返回有关失败的调用或调用远程 TAPI 方在拆解的诊断信息。

此请求使用 CO_TAPI_CALL_DIAGNOSTICS 结构，其定义，如下所示：

```c++
typedef struct _CO_TAPI_CALL_DIAGNOSTICS {
    OUT ULONG               ulOrigin;
    OUT ULONG               ulReason;
    OUT NDIS_VAR_DATA_DESC  DiagInfo;
} CO_TAPI_CALL_DIAGNOSTICS, *PCO_TAPI_CALL_DIAGNOSTICS;
```

**ulOrigin**  
指定调用的来源为以下 LINECALLORIGIN_ 常量之一： 

- **LINECALLORIGIN_OUTBOUND**  
调用是传出呼叫。

- **LINECALLORIGIN_INTERNAL**  
调用是传入和来自内部 （在相同的 PBX，例如)。

- **LINECALLORIGIN_EXTERNAL**的调用是传入和起源于外部。

- **LINECALLORIGIN_UNKNOWN**  
传入调用。 其源是当前未知但可能会变得更高版本已知。

- **LINECALLORIGIN_UNAVAIL**  
传入调用。 源不可用，并且永远不会将已知。

- **LINECALLORIGIN_CONFERENCE**  
调用句柄适用于一场电话会议-即，为与会议桥在交换机中的应用程序的连接。

**ulReason**  
指定在调用的原因为以下 LINECALLREASON_ 常量之一： 

- **LINECALLREASON_DIRECT**  
直接调用。

- **LINECALLREASON_FWDBUSY**  
调用已从忙扩展转发。

- **LINECALLREASON_FWDNOANSWER**  
调用已将转发之后一定数量的环来自未答复的扩展插件。

- **LINECALLREASON_FWDUNCOND**  
已从另一个数无条件转发调用。

- **LINECALLREASON_PICKUP**  
在调用另一个扩展从信箱接听。

- **LINECALLREASON_UNPARK**  
在调用，作为归位调用进行检索。

- **LINECALLREASON_REDIRECT**  
调用已重定向到此工作站。

- **LINECALLREASON_CALLCOMPLETION**  
在调用时调用完成请求的结果。

- **LINECALLREASON_TRANSFER**  
从另一个数转移呼叫。 参与方的标识符信息可能指示调用方是谁以及从转移呼叫。

- **LINECALLREASON_REMINDER**  
在调用是提醒你 （或"还记得"），用户必须停放的调用或在保留的时间可能很长。

- **LINECALLREASON_UNKNOWN**  
调用的原因是当前未知但可能会变得更高版本已知。

- **LINECALLREASON_UNAVAIL**  
在调用的原因不可用，并且不能变得更高版本已知。

**DiagInfo**  
指定[NDIS_VAR_DATA_DESC](https://msdn.microsoft.com/library/windows/hardware/ff559020)结构，其中包含的偏移量，以及由呼叫管理器或 MCM 驱动程序提供的可选诊断信息的长度。 内容和格式的诊断信息是驱动程序确定。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

