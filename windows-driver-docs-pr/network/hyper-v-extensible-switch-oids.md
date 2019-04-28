---
title: Hyper-V 可扩展交换机 OID
description: 本部分介绍 HYPER-V 可扩展交换机 Oid 和它们的特征。
keywords:
- Hyper-V 可扩展交换机 OID
- HYPER-V 交换机 Oid
- WDK 的 HYPER-V 可扩展交换机 Oid
- HYPER-V 可扩展交换机对象标识符
ms.assetid: A97C5BF0-7319-4BEE-ABF7-12B11CEAF3DB"
ms.date: 04/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7034925cfc6b7187bf9cacf8e49738c9952d7a67
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349527"
---
# <a name="hyper-v-extensible-switch-oids"></a>Hyper-V 可扩展交换机 OID

本部分介绍 HYPER-V 可扩展交换机对象标识符 (Oid)。 可以通过可扩展的交换机扩展或 HYPER-V 可扩展交换机扩展颁发这些 Oid。

下表定义的特征可扩展交换机 Oid。 下面的缩写形式用于在表中指定的 Oid 的特征。

- Q  
仅在查询请求中使用 OID。
- S  
仅在设置请求中使用 OID。
- M  
仅在方法请求中使用 OID。 无法对集或查询操作发出这些请求。
- P  
OID 请求颁发可扩展交换机的协议边缘。 该扩展可以检查 OID 请求以获取有关可扩展交换机，其端口或虚拟网络适配器连接到端口信息的结果。
- E  
由扩展发出 OID 请求。

| 名称                                                                                                 | Q | S | M | P | E |
|---                                                                                                   |---|---|---|---|---|
| [OID_SWITCH_FEATURE_STATUS_QUERY](https://msdn.microsoft.com/library/windows/hardware/hh598260)      |   |   | X | X |   | 
| [OID_SWITCH_NIC_ARRAY](https://msdn.microsoft.com/library/windows/hardware/hh598261)                 | X |   |   |   | X | 
| [OID_SWITCH_NIC_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)               |   | X |   | X |   |
| [OID_SWITCH_NIC_CREATE](https://msdn.microsoft.com/library/windows/hardware/hh598263)                |   | X |   | X |   |
| [OID_SWITCH_NIC_DELETE](https://msdn.microsoft.com/library/windows/hardware/hh598264)                |   | X |   | X |   |  
| [OID_SWITCH_NIC_DISCONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598265)            |   | X |   | X |   | 
| [OID_SWITCH_NIC_REQUEST](https://msdn.microsoft.com/library/windows/hardware/hh598266)               |   |   | X |   | X |   
| [OID_SWITCH_NIC_RESTORE](https://msdn.microsoft.com/library/windows/hardware/hh598267)               |   | X |   | X |   |   
| [OID_SWITCH_NIC_SAVE](https://msdn.microsoft.com/library/windows/hardware/hh598268)                  | X |   |   | X |   |
| [OID_SWITCH_NIC_SAVE_COMPLETE](https://msdn.microsoft.com/library/windows/hardware/hh598269)         |   | X |   | X |   | 
| [OID_SWITCH_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/hh598270)                | X |   |   |   | X |
| [OID_SWITCH_PORT_ARRAY](https://msdn.microsoft.com/library/windows/hardware/hh598271)                | X |   |   |   | X | 
| [OID_SWITCH_PORT_CREATE](https://msdn.microsoft.com/library/windows/hardware/hh598272)               |   | X |   | X |   | 
| [OID_SWITCH_PORT_DELETE](https://msdn.microsoft.com/library/windows/hardware/hh598273)               |   | X |   | X |   | 
| [OID_SWITCH_PORT_FEATURE_STATUS_QUERY](https://msdn.microsoft.com/library/windows/hardware/hh598274) |   |   | X | X |   | 
| [OID_SWITCH_PORT_PROPERTY_ADD](https://msdn.microsoft.com/library/windows/hardware/hh598275)         |   | X |   | X |   |
| [OID_SWITCH_PORT_PROPERTY_DELETE](https://msdn.microsoft.com/library/windows/hardware/hh598276)      |   | X |   | X |   |   
| [OID_SWITCH_PORT_PROPERTY_ENUM](https://msdn.microsoft.com/library/windows/hardware/hh598277)        |   |   | X |   | X |   
| [OID_SWITCH_PORT_PROPERTY_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598278)      |   | X |   | X |   | 
| [OID_SWITCH_PORT_TEARDOWN](https://msdn.microsoft.com/library/windows/hardware/hh598279)             |   | X |   | X |   |
| [OID_SWITCH_PROPERTY_ADD](https://msdn.microsoft.com/library/windows/hardware/hh598280)              |   | X |   | X |   | 
| [OID_SWITCH_PROPERTY_DELETE](https://msdn.microsoft.com/library/windows/hardware/hh598281)           |   | X |   | X |   | 
| [OID_SWITCH_PROPERTY_ENUM](https://msdn.microsoft.com/library/windows/hardware/hh598282)             |   |   | X |   | X |
| [OID_SWITCH_PROPERTY_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598283)           |   | X |   | X |   | 


