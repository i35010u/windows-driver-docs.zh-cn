---
title: SR-IOV OID
description: 本部分介绍 (SR-IOV) Oid 的单个根 i/o 虚拟化及其特征。
keywords:
- SR-IOV OID
- 单个根 i/o 虚拟化 Oid
- WDK SR-IOV Oid
- SR-IOV 对象标识符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dae3ad6b582d57b808044cc793fc7c99af8afb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834321"
---
# <a name="sr-iov-oids"></a>SR-IOV OID

单个根 i/o 虚拟化 (SR-IOV) 对象标识符 (Oid) 适用于支持 SR-IOV 接口的微型端口和过量驱动程序。 此接口在 NDIS 版本6.30 及更高版本中受支持。 

下表定义了 SR-IOV Oid 的特征。 以下缩写用于指定表中的 Oid 特性。

- Q  
OID 仅用于查询请求。
- S  
OID 仅用于设置请求。
- M  
OID 仅在方法请求中使用。 可以为集或查询操作发出这些请求。
- N  
OID 请求直接由 NDIS 处理，而不由微型端口驱动程序处理。 该驱动程序不会被颁发。
- P  
OID 请求仅颁发给网络适配器的物理功能 (PF) 的微型端口驱动程序。  
PF 驱动程序必须支持这些 Oid。 驱动程序还必须在 [NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的 **SupportedOidList** 成员中列出这些 oid，驱动程序在调用 [NdisMSetMiniportAttributes](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的 *MiniportAttributes* 参数中传递。
- V  
OID 请求仅颁发给某个网络的虚拟功能 (VFs) 的微型端口驱动程序。  
VF 驱动程序必须支持这些 Oid。 驱动程序还必须在 [NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的 **SupportedOidList** 成员中列出这些 oid，驱动程序在调用 [NdisMSetMiniportAttributes](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的 *MiniportAttributes* 参数中传递。

| “属性”                                                                                                 | Q | S | M | N | P | V |
|---                                                                                                   |---|---|---|---|---|---|
| [OID_NIC_SWITCH_ALLOCATE_VF](./oid-nic-switch-allocate-vf.md)           |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_CREATE_SWITCH](./oid-nic-switch-create-switch.md)         |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_CREATE_VPORT](./oid-nic-switch-create-vport.md)          |   |   | X |   | X |   |
| [OID_NIC_SWITCH_CURRENT_CAPABILITIES](./oid-nic-switch-current-capabilities.md)  | X |   |   | X |   |   |  
| [OID_NIC_SWITCH_DELETE_SWITCH](./oid-nic-switch-delete-switch.md)         |   | X |   |   | X |   |  
| [OID_NIC_SWITCH_DELETE_VPORT](./oid-nic-switch-delete-vport.md)          |   | X |   |   | X |   | 
| [OID_NIC_SWITCH_ENUM_SWITCHES](./oid-nic-switch-enum-switches.md)         | X |   |   | X |   |   |   
| [OID_NIC_SWITCH_ENUM_VFS](./oid-nic-switch-enum-vfs.md)              | X |   |   | X |   |   |   
| [OID_NIC_SWITCH_ENUM_VPORTS](./oid-nic-switch-enum-vports.md)           | X |   |   | X |   |   |  
| [OID_NIC_SWITCH_FREE_VF](./oid-nic-switch-free-vf.md)               |   | X |   |   | X |   | 
| [OID_NIC_SWITCH_HARDWARE_CAPABILITIES](./oid-nic-switch-hardware-capabilities.md) | X |   |   | X |   |   |   
| [OID_NIC_SWITCH_PARAMETERS](./oid-nic-switch-parameters.md)            |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_VF_PARAMETERS](./oid-nic-switch-vf-parameters.md)         |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_VPORT_PARAMETERS](./oid-nic-switch-vport-parameters.md)      |   |   | X |   | X |   | 
| [OID_SRIOV_BAR_RESOURCES](./oid-sriov-bar-resources.md)              |   | X |   |   | X |   | 
| [OID_SRIOV_CURRENT_CAPABILITIES](./oid-sriov-current-capabilities.md)       | X |   |   | X |   |   |   
| [OID_SRIOV_HARDWARE_CAPABILITIES](./oid-sriov-hardware-capabilities.md)      | X |   |   | X |   |   |   
| [OID_SRIOV_PF_LUID](./oid-sriov-pf-luid.md)                    | X |   |   | X |   |   |   
| [OID_SRIOV_PROBED_BARS](./oid-sriov-probed-bars.md)                | X |   |   |   | X |   | 
| [OID_SRIOV_READ_VF_CONFIG_BLOCK](./oid-sriov-read-vf-config-block.md)       |   |   | X |   | X |   | 
| [OID_SRIOV_READ_VF_CONFIG_SPACE](./oid-sriov-read-vf-config-space.md)       |   |   | X |   | X |   | 
| [OID_SRIOV_RESET_VF](./oid-sriov-reset-vf.md)                   |   | X |   |   | X |   | 
| [OID_SRIOV_SET_VF_POWER_STATE](./oid-sriov-set-vf-power-state.md)         |   | X |   |   | X |   |  
| [OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK](./oid-sriov-vf-invalidate-config-block.md) |   |   | X |   |   | X | 
| [OID_SRIOV_VF_SERIAL_NUMBER](./oid-sriov-vf-serial-number.md)           | X |   |   | X |   |   |   
| [OID_SRIOV_VF_VENDOR_DEVICE_ID](./oid-sriov-vf-vendor-device-id.md)        |   |   | X |   | X |   | 
| [OID_SRIOV_WRITE_VF_CONFIG_BLOCK](./oid-sriov-write-vf-config-block.md)      |   | X |   |   | X |   | 
| [OID_SRIOV_WRITE_VF_CONFIG_SPACE](./oid-sriov-write-vf-config-space.md)      |   | X |   |   | X |   |
