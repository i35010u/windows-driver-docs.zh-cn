---
title: OID_GEN_CO_PROTOCOL_OPTIONS
description: 本主题介绍 OID_GEN_CO_PROTOCOL_OPTIONS 对象标识符 (OID)。
ms.assetid: 5c1212e4-1fd2-435a-ae8c-9f75522cbca6
keywords:
- OID_GEN_CO_PROTOCOL_OPTIONS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0d0698b891872e151876486579c5be7b470bd7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355720"
---
# <a name="oidgencoprotocoloptions"></a>OID_GEN_CO_PROTOCOL_OPTIONS

位掩码，用于定义的协议驱动程序的可选属性。 一种协议将通知 NDIS 其属性，可以根据需要充分利用它们。 如果协议驱动程序没有在绑定上设置它的标志，NDIS 认为它们是所有明文。

当前定义的以下标志：

NDIS_PROT_OPTION_ESTIMATED_LENGTH  
指示可以指定数据包大小，而不是确切的值，此协议的最坏的情况估算值的数据包。

NDIS_PROT_OPTION_NO_LOOPBACK  
协议不需要在绑定上的环回支持。

NDIS_PROT_OPTION_NO_RSVD_ON_RCVPKT  
协议不使用**ProtocolReserved**部分指示接收数据包。 这允许 NDIS 以指示到多个协议的接收数据包。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

