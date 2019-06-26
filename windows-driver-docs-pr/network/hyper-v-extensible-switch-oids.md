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
ms.openlocfilehash: 6883f1b216449c57c9f6926434a901902e21494f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382216"
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
| [OID_SWITCH_FEATURE_STATUS_QUERY](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-feature-status-query)      |   |   | X | X |   | 
| [OID_SWITCH_NIC_ARRAY](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)                 | X |   |   |   | X | 
| [OID_SWITCH_NIC_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)               |   | X |   | X |   |
| [OID_SWITCH_NIC_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)                |   | X |   | X |   |
| [OID_SWITCH_NIC_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)                |   | X |   | X |   |  
| [OID_SWITCH_NIC_DISCONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)            |   | X |   | X |   | 
| [OID_SWITCH_NIC_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)               |   |   | X |   | X |   
| [OID_SWITCH_NIC_RESTORE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)               |   | X |   | X |   |   
| [OID_SWITCH_NIC_SAVE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)                  | X |   |   | X |   |
| [OID_SWITCH_NIC_SAVE_COMPLETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)         |   | X |   | X |   | 
| [OID_SWITCH_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-parameters)                | X |   |   |   | X |
| [OID_SWITCH_PORT_ARRAY](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-array)                | X |   |   |   | X | 
| [OID_SWITCH_PORT_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)               |   | X |   | X |   | 
| [OID_SWITCH_PORT_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)               |   | X |   | X |   | 
| [OID_SWITCH_PORT_FEATURE_STATUS_QUERY](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query) |   |   | X | X |   | 
| [OID_SWITCH_PORT_PROPERTY_ADD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)         |   | X |   | X |   |
| [OID_SWITCH_PORT_PROPERTY_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)      |   | X |   | X |   |   
| [OID_SWITCH_PORT_PROPERTY_ENUM](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)        |   |   | X |   | X |   
| [OID_SWITCH_PORT_PROPERTY_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)      |   | X |   | X |   | 
| [OID_SWITCH_PORT_TEARDOWN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)             |   | X |   | X |   |
| [OID_SWITCH_PROPERTY_ADD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)              |   | X |   | X |   | 
| [OID_SWITCH_PROPERTY_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)           |   | X |   | X |   | 
| [OID_SWITCH_PROPERTY_ENUM](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-enum)             |   |   | X |   | X |
| [OID_SWITCH_PROPERTY_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)           |   | X |   | X |   | 


