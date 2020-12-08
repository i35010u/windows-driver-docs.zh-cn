---
title: NetAdapterCx 限制
description: NetAdapterCx 限制
keywords:
- 网络适配器 WDF 类扩展限制、NetAdapterCx 限制、NetCx 限制
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4915d86fd62b11b05a9e3ab5d008a3d910c661dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840667"
---
# <a name="netadaptercx-limitations"></a>NetAdapterCx 限制

本主题介绍从 NetAdapterCx 客户端驱动程序调用 WDF 函数时应注意的注意事项。

|函数 | 描述 |
|-|-|
| [**WdfDeviceInitAssignSDDLString**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring) | 默认情况下， [**NetAdapterDeviceInitConfig**](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterdeviceinitconfig) `SDDL_DEVOBJ_SYS_ALL_ADM_RWX_WORLD_RW_RES_R` 将分配为默认 SDDL。 如果你指定限制性更强的 SDDL，则应用程序可能无法将查询 Oid 发送到适配器。 |
|[**WdfDeviceInitSetFileObjectConfig**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)| 客户端驱动程序不能在 [WDF_FILEOBJECT_CONFIG](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)的 **FileObjectClass** 成员中设置 **WdfFileObjectWdfCanUseFsContext** 。 |
| [**WdfDeviceInitAssignName**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)、 [**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)、 [**WdfDeviceInitSetDeviceType**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)、 [**WdfDeviceInitSetCharacteristics**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)、  [**WdfDeviceInitSetIoType**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)、 [**WdfDeviceInitSetPowerPageable**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable) | [**NetAdapterDeviceInitConfig**](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterdeviceinitconfig) 代表客户端驱动程序调用这些例程。 客户端驱动程序不应调用这些。
| [**WdfDeviceCreateDeviceInterface**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface) | 如果客户端驱动程序调用 [**WdfDeviceCreateDeviceInterface**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface) 且 **ReferenceString** 参数等于 **NULL**，NDIS 将截获发送到设备接口的 i/o 请求。 若要避免此行为，请指定任何引用字符串。
