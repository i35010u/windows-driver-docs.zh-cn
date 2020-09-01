---
title: OID_CO_TAPI_GET_CALL_DIAGNOSTICS
description: 本主题介绍) OID_CO_TAPI_GET_CALL_DIAGNOSTICS 对象标识符 (OID。
ms.assetid: 5b0b1a96-9d66-4ee3-9b9a-3341ca3a4b5c
keywords:
- OID_CO_TAPI_GET_CALL_DIAGNOSTICS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e133591b29980972788e789d010a93ff8168707
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206405"
---
# <a name="oid_co_tapi_get_call_diagnostics"></a>OID_CO_TAPI_GET_CALL_DIAGNOSTICS

OID_CO_TAPI_GET_CALL_DIAGNOSTICS OID 请求一个调用管理器或 MCM 驱动程序返回有关失败的调用的诊断信息或远程 TAPI 方已断开的调用。

此请求使用 CO_TAPI_CALL_DIAGNOSTICS 结构，定义如下：

```c++
typedef struct _CO_TAPI_CALL_DIAGNOSTICS {
    OUT ULONG               ulOrigin;
    OUT ULONG               ulReason;
    OUT NDIS_VAR_DATA_DESC  DiagInfo;
} CO_TAPI_CALL_DIAGNOSTICS, *PCO_TAPI_CALL_DIAGNOSTICS;
```

**ulOrigin**  
将调用的源指定为以下 LINECALLORIGIN_ 常量之一： 

- **LINECALLORIGIN_OUTBOUND**  
此调用为传出呼叫。

- **LINECALLORIGIN_INTERNAL**  
调用是传入的，并在内部 (在同一 PBX 上，例如) 。

- **LINECALLORIGIN_EXTERNAL** 调用是传入的，并从外部发出。

- **LINECALLORIGIN_UNKNOWN**  
调用是传入的。 其源目前未知，但以后可能会被识别。

- **LINECALLORIGIN_UNAVAIL**  
调用是传入的。 它的源不可用，因此永远不会被识别。

- **LINECALLORIGIN_CONFERENCE**  
调用句柄用于电话会议，即，应用程序连接到交换机中的 "网桥"。

**ulReason**  
将调用的原因指定为以下 LINECALLREASON_ 常量之一： 

- **LINECALLREASON_DIRECT**  
调用为 direct。

- **LINECALLREASON_FWDBUSY**  
调用已从繁忙的扩展中转发。

- **LINECALLREASON_FWDNOANSWER**  
从无应答扩展发送一定数量的震铃后，调用被转发。

- **LINECALLREASON_FWDUNCOND**  
此调用从另一个数字中无条件转发。

- **LINECALLREASON_PICKUP**  
从另一个扩展中选取了调用。

- **LINECALLREASON_UNPARK**  
调用被检索为寄存调用。

- **LINECALLREASON_REDIRECT**  
呼叫已重定向到此工作站。

- **LINECALLREASON_CALLCOMPLETION**  
调用是调用完成请求的结果。

- **LINECALLREASON_TRANSFER**  
调用已从另一个数字传输。 参与方标识符信息可以指示调用方是谁以及从何处传输呼叫。

- **LINECALLREASON_REMINDER**  
呼叫提醒 (或 "召回" ) 用户有可能长时间等待或处于暂停状态。

- **LINECALLREASON_UNKNOWN**  
调用的原因目前未知，但稍后可能会被识别。

- **LINECALLREASON_UNAVAIL**  
调用的原因不可用，稍后无法识别。

**DiagInfo**  
指定包含偏移量的 [NDIS_VAR_DATA_DESC](/previous-versions/windows/hardware/network/ff559020(v=vs.85)) 结构，以及由调用管理器或 MCM 驱动程序提供的可选诊断信息的长度。 诊断信息的内容和格式由驱动程序确定。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 