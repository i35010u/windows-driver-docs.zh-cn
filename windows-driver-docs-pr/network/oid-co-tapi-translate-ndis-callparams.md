---
title: OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
description: 本主题介绍 OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS 对象标识符（OID）。
ms.assetid: a56affc9-4118-4322-85bc-f979b70e0dad
keywords:
- OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad60bd6450ee31b8b9fbd5639f8d1745dbd35b87
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917513"
---
# <a name="oid_co_tapi_translate_ndis_callparams"></a>OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS

OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS OID 请求调用管理器或 MCM 驱动程序将 NDIS 调用参数（通过[CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构传递到客户端的[ProtocolClIncomingCall](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call)函数）转换为 TAPI 调用参数。 客户端使用由调用管理器或 MCM 驱动程序返回的已转换 TAPI 调用参数来确定是接受还是拒绝传入呼叫。

此请求使用 CO_TAPI_TRANSLATE_NDIS_CALLPARAMS 结构，定义如下：

```c++
typedef struct _CO_TAPI_TRANSLATE_NDIS_CALLPARAMS {
    IN  ULONG               ulFlags;
    IN  NDIS_VAR_DATA_DESC  NdisCallParams;
    OUT NDIS_VAR_DATA_DESC  LineCallInfo;
} CO_TAPI_TRANSLATE_NDIS_CALLPARAMS, *PCO_TAPI_TRANSLATE_NDIS_CALLPARAMS;
```

此结构的成员包含以下信息：

**ulFlags**  
客户端必须在**ulFlags**中设置 CO_TAPI_FLAG_INCOMING_CALL 位。

**NdisCallParams**  
指定一个[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))结构，该结构包含从 NDIS_VAR_DATA_DESC 结构开始到[CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构的偏移量。 NDIS_VAR_DATA_DESC 结构还包含 CO_CALL_PARAMETERS 结构的长度。 客户端用要转换为 TAPI 调用参数的 NDIS 调用参数填充 CO_CALL_PARAMETERS 结构。

**LineCallInfo**  
指定一个[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))结构，该结构包含从 NDIS_VAR_DATA_DESC 结构开始到 LINE_CALL_INFO 结构的偏移量。 NDIS_VAR_DATA_DESC 结构还包含 CO_CALL_PARAMETERS 结构的长度。 LINE_CALL_INFO 结构指定了向其转换给定 NDIS 调用参数的 TAPI 调用参数。 有关 LINE_CALL_INFO 结构的详细信息，请参阅 Windows SDK 和 ndistapi 头文件。

## <a name="remarks"></a>备注

如果请求成功，则调用管理器或 MCM 驱动程序将使用转换后的 TAPI 调用参数填充由**LineCallInfo**引用的 LINE_CALL_PARAMS 结构。 调用管理器或 MCM 驱动程序必须在**LineCallInfo**所引用的平面内存部分中分配 LINE_CALL_INFO 结构。 客户端将 LINE_CALL_INFO 结构的总长度写入**LineCallInfo**。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

