---
title: OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
description: 本主题介绍 OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS 对象标识符 (OID)。
ms.assetid: a56affc9-4118-4322-85bc-f979b70e0dad
keywords:
- OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9ced54e40c9f1a421a07b2f154cc7da31aecdb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380705"
---
# <a name="oidcotapitranslatendiscallparams"></a>OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS

OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS OID 请求呼叫管理器或 MCM 驱动程序将 NDIS 调用参数 (传入[CO_CALL_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff545384)客户端结构[ProtocolClIncomingCall](https://msdn.microsoft.com/library/windows/hardware/ff570228)函数) 到 TAPI 调用参数。 客户端使用返回的呼叫管理器或 MCM 驱动程序的已翻译的 TAPI 调用参数来确定是否接受或拒绝传入呼叫。

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
指定[NDIS_VAR_DATA_DESC](https://msdn.microsoft.com/library/windows/hardware/ff559020)结构，其中包含一个偏移量到 NDIS_VAR_DATA_DESC 结构的开头[CO_CALL_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff545384)结构。 NDIS_VAR_DATA_DESC 结构还包含 CO_CALL_PARAMETERS 结构的长度。 客户端填充在要转换为 TAPI 调用参数的 NDIS 调用参数 CO_CALL_PARAMETERS 结构。

**LineCallInfo**  
指定[NDIS_VAR_DATA_DESC](https://msdn.microsoft.com/library/windows/hardware/ff559020)结构，其中包含 LINE_CALL_INFO 结构从 NDIS_VAR_DATA_DESC 结构的开头的偏移量。 NDIS_VAR_DATA_DESC 结构还包含 CO_CALL_PARAMETERS 结构的长度。 LINE_CALL_INFO 结构指定到给定的 NDIS 调用参数的 TAPI 调用参数均已转换。 LINE_CALL_INFO 结构的详细信息，请参阅 Windows SDK 和 ndistapi.h 标头文件。

## <a name="remarks"></a>备注

如果请求成功，呼叫管理器或 MCM 驱动程序填充在引用该 LINE_CALL_PARAMS 结构**LineCallInfo**使用已翻译的 TAPI 调用参数。 呼叫管理器或 MCM 驱动程序必须分配中引用的平面内存部分 LINE_CALL_INFO 结构**LineCallInfo**。 客户端将写入到 LINE_CALL_INFO 结构的总长度**LineCallInfo.Length**。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

