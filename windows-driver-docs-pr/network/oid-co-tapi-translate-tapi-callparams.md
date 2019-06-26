---
title: OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS
description: 本主题介绍 OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS 对象标识符 (OID)。
ms.assetid: bee8871d-9166-4c5a-8428-964f8b321cf1
keywords:
- OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42f653a77c4d818465a6564ceca97cbb1097b586
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385505"
---
# <a name="oidcotapitranslatetapicallparams"></a>OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS

OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS OID 请求呼叫管理器或集成的调用管理器 (MCM) 微型端口驱动程序将 TAPI 调用参数为 NDIS 调用参数。 客户端查询此 OID 使用返回的 NDIS 作为输入调用参数 (格式为[CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构) 到[NdisClMakeCall](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmakecall)，与其客户端将传出呼叫。

此 OID 使用 CO_TAPI_TRANSLATE_TAPI_CALLPARAMS 结构，其定义，如下所示：

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

此结构的成员包含下列信息：

**ulLineID**  
指定传出调用将定向到的从零开始的行标识符。

**ulAddressID**  
指定的从零开始的地址标识符 (由指定的行上**ulLineID**) 到定向传出呼叫。

**ulFlags**  
客户端必须设置位 CO_TAPI_FLAG_OUTGOING_CALL **ulFlags**。 客户端可以选择性地设置位 CO_TAPI_USE_DEFAULT_CALLPARAMS **ulFlags**需要呼叫管理器或 MCM 驱动程序忽略**LineCallParams**并返回的默认 NDIS 调用参数设备。

**DestAddress**  
指定[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))格式化为字符数组的结构，其中包含目标地址从 NDIS_VAR_DATA_DESC 结构的开头的偏移量。 NDIS_VAR_DATA_DESC 结构还包含目标地址的长度。 目标地址是传出调用将定向到的地址。

**LineCallParams**  
指定[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))结构，其中包含 LINE_CALL_PARAMS 结构从 NDIS_VAR_DATA_DESC 结构的开头的偏移量。 NDIS_VAR_DATA_DESC 结构还包含 LINE_CALL_PARAMS 结构的长度。 LINE_CALL_PARAMS 结构指定要转换为 NDIS 调用参数的 TAPI 调用参数。 LINE_CALL_PARAMS 结构的详细信息，请参阅 Microsoft Windows SDK 和 ndistapi.h 标头文件。

**NdisCallParams**  
指定[NDIS_VAR_DATA_DESC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559020(v=vs.85))结构，其中包含 CO_CALL_PARAMETERS 结构从 NDIS_VAR_DATA_DESC 结构的开头的偏移量。 NDIS_VAR_DATA_DESC 结构还包含的长度[CO_CALL_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构。 CO_CALL_PARAMETERS 结构指定给定的 TAPI 调用参数均已转换到其中的 NDIS 调用参数。

## <a name="remarks"></a>备注

如果请求成功，则呼叫管理器或 MCM 驱动程序填充在 CO_CALL_PARAMETERS 结构中引用的**NdisCallParams**使用已翻译的 NDIS 调用参数。 呼叫管理器或 MCM 驱动程序必须分配中引用的平面内存部分 CO_CALL_PARAMETERS 结构**NdisCallParams**。 客户端将写入到 CO_CALL_PARAMETERS 结构的总长度**NdisCallParams.Length**。

如果客户端设置中的位 CO_TAPI_USE_DEFAULT_CALLPARAMS **ulFlags**，客户端未指定 TAPI 调用参数。 在这种情况下，呼叫管理器或 MCM 驱动程序应返回设备的默认 NDIS 调用参数。 如果设备没有默认 NDIS 调用参数，则呼叫管理器或 MCM 驱动程序应返回 NDIS_STATUS_FAILURE。


## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

