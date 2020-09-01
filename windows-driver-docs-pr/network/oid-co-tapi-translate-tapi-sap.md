---
title: OID_CO_TAPI_TRANSLATE_TAPI_SAP
description: 本主题介绍) OID_CO_TAPI_TRANSLATE_TAPI_SAP 对象标识符 (OID。
ms.assetid: 701a1d02-8528-4b61-adbb-97c817194ac7
keywords:
- OID_CO_TAPI_TRANSLATE_TAPI_SAP
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfd06f249ca2e27b88f7623339a8cbc4baf2037c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206371"
---
# <a name="oid_co_tapi_translate_tapi_sap"></a>OID_CO_TAPI_TRANSLATE_TAPI_SAP

OID_CO_TAPI_TRANSLATE_TAPI_SAP OID 请求调用管理器或集成 MCM 驱动程序，以便从 TAPI 调用参数中准备一个或多个 Sap。 查询此 OID 的客户端使用由呼叫管理器或 MCM 驱动程序返回的 NDIS SAP 作为输入 (格式设置为[NdisClRegisterSap](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)的[CO_SAP](/previous-versions/windows/hardware/network/ff545392(v=vs.85))) 结构，客户端会调用它来注册要接收传入调用的 SAP。

此请求使用 CO_TAPI_TRANSLATE_SAP 结构，定义如下：

```c++
typedef struct _CO_TAPI_TRANSLATE_SAP {
    IN  ULONG               ulLineID;
    IN  ULONG               ulAddressID;
    IN  ULONG               ulMediaModes;
    IN  ULONG               Reserved;
    OUT ULONG               NumberOfSaps;
    OUT NDIS_VAR_DATA_DESC  NdisSapParams[1];
} CO_AF_TAPI_SAP, *PCO_AF_TAPI_SAP;
```

此结构的成员包含以下信息：

**ulLineID**  
指定从零开始的行标识符。

**ulAddressID**  
指定由 **ulLineID**指定的行中的从零开始的地址标识符。

**ulMediaModes**  
指定客户端所感兴趣的信息流的媒体模式，作为以下一个或多个 LINEMEDIAMODE_constants： 

- **LINEMEDIAMODE_UNKNOWN**  
媒体流存在，但其模式目前未知，以后可能会被识别。 这对应于具有未分类媒体类型的调用。 在典型的模拟电话服务环境中，传入呼叫的媒体模式可能是未知的，直到呼叫得到应答并筛选出媒体流进行确定。 

    如果设置了 **LINEMEDIAMODE_UNKNOWN** 标志，还可以设置其他媒体标志。 这表明媒体是未知的，但它可能是其他指定媒体模式之一。

- **LINEMEDIAMODE_INTERACTIVEVOICE**  
电话上的语音能量出现，并且呼叫被视为交互式呼叫，这两个端点都是这样的。

- **LINEMEDIAMODE_AUTOMATEDVOICE**  
电话上出现语音能量，语音由自动应用程序在本地处理。

- **LINEMEDIAMODE_DATAMODEM**  
调用中的数据调制解调器会话。

- **LINEMEDIAMODE_G3FAX**  
通过呼叫发送或接收组3传真。

- **LINEMEDIAMODE_G4FAX**  
通过呼叫发送或接收组4传真。

- **LINEMEDIAMODE_TDD**  
一个 TDD (电信设备，用于呼叫上的失聪) 会话。

- **LINEMEDIAMODE_DIGITALDATA**  
通过呼叫发送或接收数字数据。

- **LINEMEDIAMODE_TELETEX**  
调用上的 teletex 会话。  (Teletex 是 telematic services 之一。 ) 

- **LINEMEDIAMODE_VIDEOTEX**  
调用上的 videotex 会话。  (Videotex 是 telematic services 中的一个。 ) 

- **LINEMEDIAMODE_TELEX**  
调用上的电传会话。  (电传是 telematic services 之一 ) 

- **LINEMEDIAMODE_MIXED**  
调用时的混合会话。  (Mixed 是 ISDN telematic services 之一。 ) 

- **LINEMEDIAMODE_ADSI**  
ADSI (模拟显示服务接口) 会话上的会话。

- **LINEMEDIAMODE_VOICEVIEW**  
调用的媒体模式为 VoiceView。

**预留**  
这是保留的。 客户端必须将此字段设置为0。

**NumberOfSaps**  
指定**NdisSapParams**中包含在缓冲区中的[NDIS_VAR_DATA_DESC](/previous-versions/windows/hardware/network/ff559020(v=vs.85))结构的数目。

**NdisSapParams**  
指定包含一个或多个 NDIS_VAR_DATA_DESC 结构的可变长度数组。 每个 NDIS_VAR_DATA_DESC 结构都包含一个到 [CO_SAP](/previous-versions/windows/hardware/network/ff545392(v=vs.85)) 结构的偏移量以及长度。 每个 CO_SAP 结构指定一个服务访问点 (SAP) ，面向连接的客户端可以在该点上接收传入呼叫。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 