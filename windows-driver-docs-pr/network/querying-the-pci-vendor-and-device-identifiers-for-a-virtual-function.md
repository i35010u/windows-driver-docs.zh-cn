---
title: 查询虚拟功能的 PCI 供应商和设备 Id
description: 查询虚拟功能的 PCI 供应商和设备标识符
ms.assetid: A2FB0A35-A89B-4028-92BA-E75739B080FD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4430d9b78e94a6b495d037c840f6fb692c35b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844868"
---
# <a name="querying-the-pci-vendor-and-device-identifiers-for-a-virtual-function"></a>查询虚拟功能的 PCI 供应商和设备标识符

**注意**此方法只能由 Hyper-v 父分区的管理操作系统中运行的过量驱动程序使用。

过量驱动程序发出[OID\_SRIOV\_VF\_供应商\_设备\_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-vendor-device-id)的对象标识符（oid）方法请求，以查询 PCI Express （PCIe）供应商标识符（*VendorID*）和设备标识符（*DeviceID*）。 此数据是从适用于物理网络适配器上的 PCIe 虚拟功能（VF）的 PCIe 配置空间读取的。

过量驱动程序将此 OID 方法请求发送到网络适配器 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序。 对于支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 小型端口驱动程序，此 OID 方法请求是必需的。

在 Hyper-v 子分区中运行的来宾操作系统为设备枚举的泛型即插即用（PnP） Id 使用了 VF 和 VF 的 DeviceID。 从 Windows Server 2012 开始，PF 微型端口驱动程序可以为子分区中公开的 VF 网络适配器提供以下一组标识符：

-   物理网络适配器的 VendorID 和 DeviceID。 这允许将兼容的驱动程序加载到在 Hyper-v 子分区中运行的来宾操作系统中，以及在 Hyper-v 父分区中运行的管理操作系统。

-   与物理网络适配器的标识符不同的 VendorID 和 DeviceID。 这允许在来宾操作系统中加载驱动程序，该驱动程序更适合于其用途。 例如，PF 小型端口驱动程序可能会为 VF 网络适配器返回一个 VendorID 和 DeviceID，以便加载用于禁用某些功能集（如电源管理或协议任务卸载）的驱动程序。

在发出此 OID 方法请求之前，过量驱动程序必须[ **\_供应商\_设备\_ID\_INFO 结构初始化 NDIS\_SRIOV\_VF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info) 。 驱动程序必须将**VFId**成员设置为要从中读取信息的 VF 的标识符。

当它处理此 OID 请求时，PF 微型端口驱动程序必须验证指定的 VF 是否包含以前分配的资源。 在 oid 的 OID 方法请求中，PF 微型端口驱动程序为一个 VF 分配资源[\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

 

 





