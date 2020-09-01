---
title: 查询虚拟功能的 PCI 供应商和设备 Id
description: 查询虚拟功能的 PCI 供应商和设备标识符
ms.assetid: A2FB0A35-A89B-4028-92BA-E75739B080FD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8122c2deca2c435d92be748036903172905f7ed
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216968"
---
# <a name="querying-the-pci-vendor-and-device-identifiers-for-a-virtual-function"></a>查询虚拟功能的 PCI 供应商和设备标识符

**注意** 此方法只能由 Hyper-v 父分区的管理操作系统中运行的过量驱动程序使用。

过量驱动程序发出对象标识符 (oid) 方法请求 [oid \_ SRIOV \_ VF \_ 供应商 \_ 设备 \_ ID](./oid-sriov-vf-vendor-device-id.md) ，以查询 PCI Express (PCIe) 供应商 *标识符 (DeviceID) 和* 设备标识符 (*DeviceID*) 。 此数据是从 pcie 虚拟功能的 PCIe 配置空间读取的， (VF) 在物理网络适配器上。

过量驱动程序将此 OID 方法请求发送到 PCI Express (PCIe 的微型端口驱动程序) 物理功能 (PF) 网络适配器。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 方法请求。

在 Hyper-v 子分区中运行的来宾操作系统使用适用于泛型即插即用的 VF 的 VendorID 和 DeviceID (用于设备枚举的 PnP) Id。 从 Windows Server 2012 开始，PF 微型端口驱动程序可以为子分区中公开的 VF 网络适配器提供以下一组标识符：

-   物理网络适配器的 VendorID 和 DeviceID。 这允许将兼容的驱动程序加载到在 Hyper-v 子分区中运行的来宾操作系统中，以及在 Hyper-v 父分区中运行的管理操作系统。

-   与物理网络适配器的标识符不同的 VendorID 和 DeviceID。 这允许在来宾操作系统中加载驱动程序，该驱动程序更适合于其用途。 例如，PF 小型端口驱动程序可能会为 VF 网络适配器返回一个 VendorID 和 DeviceID，以便加载用于禁用某些功能集（如电源管理或协议任务卸载）的驱动程序。

在发出此 OID 方法请求之前，过量驱动程序必须初始化 [**NDIS \_ SRIOV \_ VF \_ 供应商 \_ 设备 \_ ID \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info) 结构。 驱动程序必须将 **VFId** 成员设置为要从中读取信息的 VF 的标识符。

当它处理此 OID 请求时，PF 微型端口驱动程序必须验证指定的 VF 是否包含以前分配的资源。 在 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md)的 oid 方法请求期间，PF 微型端口驱动程序为 VF 分配资源。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

 

