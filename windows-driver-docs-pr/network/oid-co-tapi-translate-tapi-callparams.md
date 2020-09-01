---
title: OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS
description: 本主题介绍) OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS 对象标识符 (OID。
ms.assetid: bee8871d-9166-4c5a-8428-964f8b321cf1
keywords:
- OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: eba64fe2046a3e4a7473980b5b33e2e35d3b6d0d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206369"
---
# <a name="oid_co_tapi_translate_tapi_callparams"></a>OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS

OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS OID 请求呼叫管理器或集成的呼叫管理器微型端口 (MCM) 驱动程序，将 TAPI 调用参数转换为 NDIS 调用参数。 查询此 OID 的客户端使用返回的 NDIS 调用参数作为输入 (，并将其设置为 [CO_CALL_PARAMETERS](/previous-versions/windows/hardware/network/ff545384(v=vs.85)) 结构) 到 [NdisClMakeCall](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)，以便客户端发出传出调用。

此 OID 使用 CO_TAPI_TRANSLATE_TAPI_CALLPARAMS 结构，定义如下：

```c++
typedef struct _CO_TAPI_TRANSLATE_TAPI_CALLPARAMS {
    IN  ULONG               ulLineID;
    IN  ULONG               ulAddressID;
    IN  ULONG               ulFlags;
    IN  NDIS_VAR_DATA_DESC  DestAddress;
    IN  NDIS_VAR_DATA_DESC  LineCallParams;
    OUT NDIS_VAR_DATA_DESC  NdisCallParams;
} CO_TAPI_TRANSLATE_TAPI_CALLPARAMS, *PCO_TAPI_TRANSLATE_TAPI_CALLPARAMS;
```

此结构的成员包含以下信息：

**ulLineID**  
指定一个从零开始的行标识符，传出调用将定向到该标识符。

**ulAddressID**  
指定由 **ulLineID** 指定的行上从零开始的地址标识符 () 由传出调用定向到的行。

**ulFlags**  
客户端必须在 **ulFlags**中设置 CO_TAPI_FLAG_OUTGOING_CALL 位。 客户端可以选择将 **ulFlags** 中的 CO_TAPI_USE_DEFAULT_CALLPARAMS 位设置为要求调用管理器或 MCM 驱动程序忽略 **LineCallParams** ，并为设备返回默认的 NDIS 调用参数。

**DestAddress**  
指定一个 [NDIS_VAR_DATA_DESC](/previous-versions/windows/hardware/network/ff559020(v=vs.85)) 结构，该结构包含从 NDIS_VAR_DATA_DESC 结构开始到格式化为字符数组的目标地址的偏移量。 NDIS_VAR_DATA_DESC 结构还包含目标地址的长度。 目标地址是传出调用将定向到的地址。

**LineCallParams**  
指定一个 [NDIS_VAR_DATA_DESC](/previous-versions/windows/hardware/network/ff559020(v=vs.85)) 结构，该结构包含从 NDIS_VAR_DATA_DESC 结构开始到 LINE_CALL_PARAMS 结构的偏移量。 NDIS_VAR_DATA_DESC 结构还包含 LINE_CALL_PARAMS 结构的长度。 LINE_CALL_PARAMS 结构指定要转换为 NDIS 调用参数的 TAPI 调用参数。 有关 LINE_CALL_PARAMS 结构的详细信息，请参阅 Microsoft Windows SDK 和 ndistapi 头文件。

**NdisCallParams**  
指定一个 [NDIS_VAR_DATA_DESC](/previous-versions/windows/hardware/network/ff559020(v=vs.85)) 结构，该结构包含从 NDIS_VAR_DATA_DESC 结构开始到 CO_CALL_PARAMETERS 结构的偏移量。 NDIS_VAR_DATA_DESC 结构还包含 [CO_CALL_PARAMETERS](/previous-versions/windows/hardware/network/ff545384(v=vs.85)) 结构的长度。 CO_CALL_PARAMETERS 结构指定了向其转换给定 TAPI 调用参数的 NDIS 调用参数。

## <a name="remarks"></a>备注

如果请求成功，则调用管理器或 MCM 驱动程序将使用转换后的 NDIS 调用参数填充 **NdisCallParams** 所引用的 CO_CALL_PARAMETERS 结构。 调用管理器或 MCM 驱动程序必须在 **NdisCallParams**所引用的平面内存部分中分配 CO_CALL_PARAMETERS 结构。 客户端将 CO_CALL_PARAMETERS 结构的总长度写入 **NdisCallParams**。

如果客户端设置 **ulFlags**中的 CO_TAPI_USE_DEFAULT_CALLPARAMS 位，则客户端不会指定 TAPI 调用参数。 在这种情况下，呼叫管理器或 MCM 驱动程序应为设备返回默认的 NDIS 调用参数。 如果设备没有默认的 NDIS 调用参数，则调用管理器或 MCM 驱动程序应返回 NDIS_STATUS_FAILURE。


## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 