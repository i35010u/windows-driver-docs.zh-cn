---
title: Hyper-V 可扩展交换机 OID
description: 本部分介绍 Hyper-v 可扩展交换机 Oid 及其特性。
keywords:
- Hyper-V 可扩展交换机 OID
- Hyper-v 交换机 Oid
- WDK Hyper-v 可扩展交换机 Oid
- Hyper-v 可扩展交换机对象标识符
ms.assetid: A97C5BF0-7319-4BEE-ABF7-12B11CEAF3DB"
ms.date: 04/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 227f6799d2574984f419d5c698ff3fc034356ecf
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211045"
---
# <a name="hyper-v-extensible-switch-oids"></a>Hyper-V 可扩展交换机 OID

本节介绍 Hyper-v 可扩展交换机对象标识符 (Oid) 。 这些 Oid 可能由可扩展交换机扩展或 Hyper-v 可扩展交换机扩展颁发。

下表定义了可扩展交换机 Oid 的特征。 以下缩写用于指定表中的 Oid 特性。

- Q  
OID 仅用于查询请求。
- S  
OID 仅用于设置请求。
- M  
OID 仅在方法请求中使用。 可以为集或查询操作发出这些请求。
- P  
OID 请求由可扩展交换机的协议边缘发出。 扩展可以检查 OID 请求的结果，以获取有关可扩展交换机、其端口或连接到端口的虚拟网络适配器的信息。
- E  
OID 请求由扩展发出。

| 名称                                                                                                 | Q | S | M | P | E |
|---                                                                                                   |---|---|---|---|---|
| [OID_SWITCH_FEATURE_STATUS_QUERY](./oid-switch-feature-status-query.md)      |   |   | X | X |   | 
| [OID_SWITCH_NIC_ARRAY](./oid-switch-nic-array.md)                 | X |   |   |   | X | 
| [OID_SWITCH_NIC_CONNECT](./oid-switch-nic-connect.md)               |   | X |   | X |   |
| [OID_SWITCH_NIC_CREATE](./oid-switch-nic-create.md)                |   | X |   | X |   |
| [OID_SWITCH_NIC_DELETE](./oid-switch-nic-delete.md)                |   | X |   | X |   |  
| [OID_SWITCH_NIC_DISCONNECT](./oid-switch-nic-disconnect.md)            |   | X |   | X |   | 
| [OID_SWITCH_NIC_REQUEST](./oid-switch-nic-request.md)               |   |   | X |   | X |   
| [OID_SWITCH_NIC_RESTORE](./oid-switch-nic-restore.md)               |   | X |   | X |   |   
| [OID_SWITCH_NIC_SAVE](./oid-switch-nic-save.md)                  | X |   |   | X |   |
| [OID_SWITCH_NIC_SAVE_COMPLETE](./oid-switch-nic-save-complete.md)         |   | X |   | X |   | 
| [OID_SWITCH_PARAMETERS](./oid-switch-parameters.md)                | X |   |   |   | X |
| [OID_SWITCH_PORT_ARRAY](./oid-switch-port-array.md)                | X |   |   |   | X | 
| [OID_SWITCH_PORT_CREATE](./oid-switch-port-create.md)               |   | X |   | X |   | 
| [OID_SWITCH_PORT_DELETE](./oid-switch-port-delete.md)               |   | X |   | X |   | 
| [OID_SWITCH_PORT_FEATURE_STATUS_QUERY](./oid-switch-port-feature-status-query.md) |   |   | X | X |   | 
| [OID_SWITCH_PORT_PROPERTY_ADD](./oid-switch-port-property-add.md)         |   | X |   | X |   |
| [OID_SWITCH_PORT_PROPERTY_DELETE](./oid-switch-port-property-delete.md)      |   | X |   | X |   |   
| [OID_SWITCH_PORT_PROPERTY_ENUM](./oid-switch-port-property-enum.md)        |   |   | X |   | X |   
| [OID_SWITCH_PORT_PROPERTY_UPDATE](./oid-switch-port-property-update.md)      |   | X |   | X |   | 
| [OID_SWITCH_PORT_TEARDOWN](./oid-switch-port-teardown.md)             |   | X |   | X |   |
| [OID_SWITCH_PROPERTY_ADD](./oid-switch-property-add.md)              |   | X |   | X |   | 
| [OID_SWITCH_PROPERTY_DELETE](./oid-switch-property-delete.md)           |   | X |   | X |   | 
| [OID_SWITCH_PROPERTY_ENUM](./oid-switch-property-enum.md)             |   |   | X |   | X |
| [OID_SWITCH_PROPERTY_UPDATE](./oid-switch-property-update.md)           |   | X |   | X |   |