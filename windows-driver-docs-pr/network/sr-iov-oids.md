---
title: SR-IOV OID
description: 本部分介绍单根 I/O 虚拟化 (SR-IOV) Oid 和它们的特征。
keywords:
- SR-IOV OID
- 单根 I/O 虚拟化 Oid
- WDK 的 SR-IOV Oid
- SR-IOV 对象标识符
ms.assetid: E93751BF-17BC-4BE7-89F7-53F6C9941120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8d5b7e6859fe087c90e155432c63483bbc57e6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386210"
---
# <a name="sr-iov-oids"></a>SR-IOV OID

单根 I/O 虚拟化 (SR-IOV) 对象标识符 (Oid) 适用于微型端口和基础驱动程序支持 SR-IOV 的接口。 在 NDIS 版本 6.30 和更高版本中支持此接口。 

下表定义的 SR-IOV Oid 的特征。 下面的缩写形式用于在表中指定的 Oid 的特征。

- Q  
仅在查询请求中使用 OID。
- S  
仅在设置请求中使用 OID。
- M  
仅在方法请求中使用 OID。 无法对集或查询操作发出这些请求。
- N  
OID 请求直接由 NDIS 而不是由微型端口驱动程序处理。 该驱动程序将不会颁发这些 Oid。
- P  
仅对网络适配器的物理函数 (PF) 的微型端口驱动程序发出 OID 请求。  
PF 驱动程序必须支持这些 Oid。 该驱动程序还必须列出在这些 Oid **SupportedOidList**的成员[NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)驱动程序中传递的结构*MiniportAttributes*到调用的参数[NdisMSetMiniportAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)。
- V  
仅对网络的虚拟函数 (VFs) 之一的微型端口驱动程序发出 OID 请求。  
VF 驱动程序必须支持这些 Oid。 该驱动程序还必须列出在这些 Oid **SupportedOidList**的成员[NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)驱动程序中传递的结构*MiniportAttributes*到调用的参数[NdisMSetMiniportAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)。

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


