---
title: SR-IOV OID
description: 本部分介绍单根 i/o 虚拟化（SR-IOV） Oid 及其特性。
keywords:
- SR-IOV OID
- 单个根 i/o 虚拟化 Oid
- WDK SR-IOV Oid
- SR-IOV 对象标识符
ms.assetid: E93751BF-17BC-4BE7-89F7-53F6C9941120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e39b18ffd6943437503245607820e8951b69f21
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841857"
---
# <a name="sr-iov-oids"></a>SR-IOV OID

单个根 i/o 虚拟化（SR-IOV）对象标识符（Oid）适用于支持 SR-IOV 接口的微型端口和过量驱动程序。 此接口在 NDIS 版本6.30 及更高版本中受支持。 

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
OID 请求仅颁发给网络适配器的物理功能（PF）的微型端口驱动程序。  
PF 驱动程序必须支持这些 Oid。 驱动程序还必须在[NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的**SupportedOidList**成员中列出这些 oid，驱动程序在调用 [的 MiniportAttributes 参数中传递NdisMSetMiniportAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)。
- V  
OID 请求仅颁发给某个网络虚函数（VFs）的微型端口驱动程序。  
VF 驱动程序必须支持这些 Oid。 驱动程序还必须在[NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的**SupportedOidList**成员中列出这些 oid，驱动程序在调用 [的 MiniportAttributes 参数中传递NdisMSetMiniportAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)。

| 名称                                                                                                 | Q | S | M | N | P | V |
|---                                                                                                   |---|---|---|---|---|---|
| [OID_NIC_SWITCH_ALLOCATE_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)           |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_CREATE_SWITCH](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)         |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_CREATE_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)          |   |   | X |   | X |   |
| [OID_NIC_SWITCH_CURRENT_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-current-capabilities)  | X |   |   | X |   |   |  
| [OID_NIC_SWITCH_DELETE_SWITCH](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)         |   | X |   |   | X |   |  
| [OID_NIC_SWITCH_DELETE_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)          |   | X |   |   | X |   | 
| [OID_NIC_SWITCH_ENUM_SWITCHES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)         | X |   |   | X |   |   |   
| [OID_NIC_SWITCH_ENUM_VFS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)              | X |   |   | X |   |   |   
| [OID_NIC_SWITCH_ENUM_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)           | X |   |   | X |   |   |  
| [OID_NIC_SWITCH_FREE_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)               |   | X |   |   | X |   | 
| [OID_NIC_SWITCH_HARDWARE_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-hardware-capabilities) | X |   |   | X |   |   |   
| [OID_NIC_SWITCH_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)            |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_VF_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)         |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_VPORT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)      |   |   | X |   | X |   | 
| [OID_SRIOV_BAR_RESOURCES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-bar-resources)              |   | X |   |   | X |   | 
| [OID_SRIOV_CURRENT_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-current-capabilities)       | X |   |   | X |   |   |   
| [OID_SRIOV_HARDWARE_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-hardware-capabilities)      | X |   |   | X |   |   |   
| [OID_SRIOV_PF_LUID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-pf-luid)                    | X |   |   | X |   |   |   
| [OID_SRIOV_PROBED_BARS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-probed-bars)                | X |   |   |   | X |   | 
| [OID_SRIOV_READ_VF_CONFIG_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-block)       |   |   | X |   | X |   | 
| [OID_SRIOV_READ_VF_CONFIG_SPACE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)       |   |   | X |   | X |   | 
| [OID_SRIOV_RESET_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)                   |   | X |   |   | X |   | 
| [OID_SRIOV_SET_VF_POWER_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-set-vf-power-state)         |   | X |   |   | X |   |  
| [OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-invalidate-config-block) |   |   | X |   |   | X | 
| [OID_SRIOV_VF_SERIAL_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-serial-number)           | X |   |   | X |   |   |   
| [OID_SRIOV_VF_VENDOR_DEVICE_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-vendor-device-id)        |   |   | X |   | X |   | 
| [OID_SRIOV_WRITE_VF_CONFIG_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-block)      |   | X |   |   | X |   | 
| [OID_SRIOV_WRITE_VF_CONFIG_SPACE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-space)      |   | X |   |   | X |   |


