---
title: OID_GEN_CO_PROTOCOL_OPTIONS
description: 本主题介绍 OID_GEN_CO_PROTOCOL_OPTIONS 对象标识符（OID）。
ms.assetid: 5c1212e4-1fd2-435a-ae8c-9f75522cbca6
keywords:
- OID_GEN_CO_PROTOCOL_OPTIONS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2b3bca6ee5dc9e76646bc1759f472c77d92b2f9
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917493"
---
# <a name="oid_gen_co_protocol_options"></a>OID_GEN_CO_PROTOCOL_OPTIONS

一个位掩码，用于定义协议驱动程序的可选属性。 协议会将其属性告知 NDIS，可以选择利用它们。 如果协议驱动程序没有在绑定上设置其标志，NDIS 会假设它们全都清楚。

当前定义了下列标志：

NDIS_PROT_OPTION_ESTIMATED_LENGTH  
指示在此协议的数据包大小的最差情况下（而不是精确值）可以指示数据包。

NDIS_PROT_OPTION_NO_LOOPBACK  
协议不需要对绑定的环回支持。

NDIS_PROT_OPTION_NO_RSVD_ON_RCVPKT  
协议不使用所指示的接收数据包的**ProtocolReserved**部分。 这允许 NDIS 将接收数据包指示到多个协议。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

