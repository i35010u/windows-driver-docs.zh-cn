---
title: OID_CO_TAPI_TRANSLATE_TAPI_SAP
description: 本主题介绍 OID_CO_TAPI_TRANSLATE_TAPI_SAP 对象标识符 (OID)。
ms.assetid: 701a1d02-8528-4b61-adbb-97c817194ac7
keywords:
- OID_CO_TAPI_TRANSLATE_TAPI_SAP
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: b15fd2a12a55088c3667d1dbbc6edca93e6748e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380700"
---
# <a name="oidcotapitranslatetapisap"></a>OID_CO_TAPI_TRANSLATE_TAPI_SAP

OID_CO_TAPI_TRANSLATE_TAPI_SAP OID 请求要准备从 TAPI 调用参数的一个或多个 SAPs 的呼叫管理器或 MCM 的集成驱动程序。 查询此 OID 的客户端使用 NDIS SAP 返回的呼叫管理器或作为输入的 MCM 驱动程序 (格式为[CO_SAP](https://msdn.microsoft.com/library/windows/hardware/ff545392)结构) 到[NdisClRegisterSap](https://msdn.microsoft.com/library/windows/hardware/ff561648)，该客户端调用上注册 SAP要接收传入的呼叫。

此请求使用 CO_TAPI_TRANSLATE_SAP 结构，其定义，如下所示：

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

此结构的成员包含下列信息：

**ulLineID**  
指定的从零开始的行标识符。

**ulAddressID**  
通过指定的行上指定的从零开始的地址标识符**ulLineID**。

**ulMediaModes**  
指定的调用的客户端很感兴趣，作为一个或多个以下 LINEMEDIAMODE_constants 信息流的媒体模式： 

- **LINEMEDIAMODE_UNKNOWN**  
媒体流存在，但其模式是当前未知的可能会变得更高版本已知。 这对应于具有未分类的媒体类型的调用。 在典型的模拟电话服务环境中的传入呼叫的媒体模式可能未知直到后应答呼叫和已筛选的媒体流来确定。 

    如果**LINEMEDIAMODE_UNKNOWN**设置标志，还可以设置其他媒体标志。 这表示媒体是未知但可能需要其他指示的媒体模式之一。

- **LINEMEDIAMODE_INTERACTIVEVOICE**  
语音能源上调用，并调用存在被视为具有两个边界的人类的交互式调用。

- **LINEMEDIAMODE_AUTOMATEDVOICE**  
通过自动化应用程序本地处理的调用和语音的语音能源状态。

- **LINEMEDIAMODE_DATAMODEM**  
在调用数据调制解调器会话。

- **LINEMEDIAMODE_G3FAX**  
组 3 传真正在通过调用发送或接收。

- **LINEMEDIAMODE_G4FAX**  
正在组 4 传真发送或接收通过调用。

- **LINEMEDIAMODE_TDD**  
在调用一个 TDD （对于失聪电信设备） 会话。

- **LINEMEDIAMODE_DIGITALDATA**  
数字数据正在通过调用发送或接收。

- **LINEMEDIAMODE_TELETEX**  
在调用 teletex 会话。 （Teletex 是信息通讯业务服务之一。）

- **LINEMEDIAMODE_VIDEOTEX**  
在调用 videotex 会话。 (Videotex 是一个信息通讯业务服务。)

- **LINEMEDIAMODE_TELEX**  
在调用电报会话。 （电报是信息通讯业务服务之一。）

- **LINEMEDIAMODE_MIXED**  
在调用混合的会话。 （混合是 ISDN 信息通讯业务服务之一。）

- **LINEMEDIAMODE_ADSI**  
在调用 ADSI （模拟显示服务接口） 会话。

- **LINEMEDIAMODE_VOICEVIEW**  
在调用媒体模式下是 VoiceView。

**保留**  
这会保留。 客户端必须将此字段设置为 0。

**NumberOfSaps**  
指定的数量[NDIS_VAR_DATA_DESC](https://msdn.microsoft.com/library/windows/hardware/ff559020)缓冲区中包含结构**NdisSapParams**。

**NdisSapParams**  
指定包含一个或多个 NDIS_VAR_DATA_DESC 结构的变长数组。 每个 NDIS_VAR_DATA_DESC 结构包含的偏移量，以及的长度[CO_SAP](https://msdn.microsoft.com/library/windows/hardware/ff545392)结构。 每个 CO_SAP 结构指定的面向连接的客户端可以接收传入调用的服务访问点 (SAP)。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

