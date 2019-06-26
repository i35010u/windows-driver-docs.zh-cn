---
title: OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
description: 本主题介绍 OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS 对象标识符 (OID)。
ms.assetid: a56affc9-4118-4322-85bc-f979b70e0dad
keywords:
- OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e86a743e2328344a8194fb200c2753dc23773b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385508"
---
# <a name="oidcotapitranslatendiscallparams"></a>OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS

OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS OID 请求呼叫管理器或 MCM 驱动程序将 NDIS 调用参数 (传入[CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))客户端结构[ProtocolClIncomingCall](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_incoming_call)函数) 到 TAPI 调用参数。 客户端使用返回的呼叫管理器或 MCM 驱动程序的已翻译的 TAPI 调用参数来确定是否接受或拒绝传入呼叫。

此请求使用 CO_TAPI_TRANSLATE_NDIS_CALLPARAMS 结构，其定义，如下所示：

```c++
typedef struct _CO_TAPI_TRANSLATE_NDIS_CALLPARAMS {
    IN  ULONG               ulFlags;
    IN  NDIS_VAR_DATA_DESC  NdisCallParams;
    OUT NDIS_VAR_DATA_DESC  LineCallInfo;
} CO_TAPI_TRANSLATE_NDIS_CALLPARAMS, *PCO_TAPI_TRANSLATE_NDIS_CALLPARAMS;
```

此结构的成员包含下列信息：

**ulFlags**  
客户端必须设置位 CO_TAPI_FLAG_INCOMING_CALL **ulFlags**。

**NdisCallParams**  
指定[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))结构，其中包含一个偏移量到 NDIS_VAR_DATA_DESC 结构的开头[CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构。 NDIS_VAR_DATA_DESC 结构还包含 CO_CALL_PARAMETERS 结构的长度。 客户端填充在要转换为 TAPI 调用参数的 NDIS 调用参数 CO_CALL_PARAMETERS 结构。

**LineCallInfo**  
指定[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))结构，其中包含 LINE_CALL_INFO 结构从 NDIS_VAR_DATA_DESC 结构的开头的偏移量。 NDIS_VAR_DATA_DESC 结构还包含 CO_CALL_PARAMETERS 结构的长度。 LINE_CALL_INFO 结构指定到给定的 NDIS 调用参数的 TAPI 调用参数均已转换。 LINE_CALL_INFO 结构的详细信息，请参阅 Windows SDK 和 ndistapi.h 标头文件。

## <a name="remarks"></a>备注

如果请求成功，呼叫管理器或 MCM 驱动程序填充在引用该 LINE_CALL_PARAMS 结构**LineCallInfo**使用已翻译的 TAPI 调用参数。 呼叫管理器或 MCM 驱动程序必须分配中引用的平面内存部分 LINE_CALL_INFO 结构**LineCallInfo**。 客户端将写入到 LINE_CALL_INFO 结构的总长度**LineCallInfo.Length**。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

