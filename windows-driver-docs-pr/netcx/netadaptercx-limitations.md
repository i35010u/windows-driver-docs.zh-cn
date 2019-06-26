---
title: NetAdapterCx 限制
description: NetAdapterCx 限制
ms.assetid: 2333F2D9-A369-4124-9365-ABC49E8B5595
keywords:
- 网络适配器 WDF 类扩展限制，NetAdapterCx 限制，NetCx 限制
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a2d3c13a895607ccfc56399f385c9878728c79f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382824"
---
# <a name="netadaptercx-limitations"></a>NetAdapterCx 限制

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

本主题介绍你应注意从 NetAdapterCx 客户端驱动程序调用 WDF 函数时需要注意的问题。

|函数 | 描述 |
|-|-|
| [**WdfDeviceInitAssignSDDLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring) | 默认情况下[ **NetAdapterDeviceInitConfig** ](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)分配`SDDL_DEVOBJ_SYS_ALL_ADM_RWX_WORLD_RW_RES_R`作为默认 SDDL。 如果指定限制性更强的 SDDL，应用程序可能无法向适配器发送查询 Oid。 |
|[**WdfDeviceInitSetFileObjectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)| 不能设置客户端驱动程序**WdfFileObjectWdfCanUseFsContext**中**FileObjectClass**的成员[WDF_FILEOBJECT_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)。 |
| [**WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)， [ **WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)， [ **WdfDeviceInitSetDeviceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)， [ **WdfDeviceInitSetCharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)， [ **WdfDeviceInitSetIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)， [ **WdfDeviceInitSetPowerPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable) | [**NetAdapterDeviceInitConfig** ](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)代表客户端驱动程序调用这些例程。 客户端驱动程序不应调用它们。
| [**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface) | 如果客户端驱动程序调用[ **WdfDeviceCreateDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)与**ReferenceString**参数等于**NULL**，NDIS截获发送到设备接口的 I/O 请求。 若要避免此行为，指定引用的任何字符串。
