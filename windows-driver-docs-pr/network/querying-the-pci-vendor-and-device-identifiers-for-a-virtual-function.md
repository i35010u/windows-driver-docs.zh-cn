---
title: 查询虚拟函数的 PCI 供应商和设备 Id
description: 查询虚拟功能的 PCI 供应商和设备标识符
ms.assetid: A2FB0A35-A89B-4028-92BA-E75739B080FD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cd48b27dc3abf8e377c50910adc65473fafe9ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377039"
---
# <a name="querying-the-pci-vendor-and-device-identifiers-for-a-virtual-function"></a>查询虚拟功能的 PCI 供应商和设备标识符

**请注意**此方法只能由过量的 HYPER-V 父分区在管理操作系统中运行的驱动程序。

基础驱动程序发出的一个对象标识符 (OID) 方法请求[OID\_SRIOV\_VF\_供应商\_设备\_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-vendor-device-id)查询 PCI Express (PCIe) 供应商标识符 (*VendorID*) 和设备标识符 (*DeviceID*)。 此数据从 PCIe 配置空间为 PCIe 虚拟函数 (VF) 物理网络适配器上读取。

基础驱动程序微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 的网络适配器向颁发此 OID 方法请求。 此 OID 方法请求是必需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。

来宾操作系统，它运行的 HYPER-V 子分区中，使用设备枚举的泛型和插即用 (PnP) id VendorID 和的 VF 设备 Id。 从 Windows Server 2012 开始，PF 微型端口驱动程序可以在子分区中公开的 VF 网络适配器提供以下一组标识符：

-   VendorID 和物理网络适配器的 DeviceID。 这允许兼容的驱动程序才能加载到运行 HYPER-V 子分区中，来宾操作系统和管理操作系统，它运行在 HYPER-V 父分区中。

-   VendorID 和设备 Id 不同于物理网络适配器的标识符。 这样更适合使用来宾操作系统中加载的驱动程序。 例如，PF 微型端口驱动程序可能会返回 VendorID 和 DeviceID VF 网络适配器，以便加载驱动程序，以禁用某些功能集，如电源管理或协议任务将卸载。

它会发出此 OID 方法请求之前，必须初始化基础驱动程序[ **NDIS\_SRIOV\_VF\_供应商\_设备\_ID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)结构。 该驱动程序必须设置**VFId** VF 是要读取信息的标识符的成员。

当它处理此 OID 请求时，PF 微型端口驱动程序必须验证指定的 VF 具有先前已分配的资源。 PF 微型端口驱动程序 OID 方法请求的过程将资源分配的 VF [OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。 如果尚未分配指定 VF 的资源的驱动程序必须失败 OID 请求。

 

 





