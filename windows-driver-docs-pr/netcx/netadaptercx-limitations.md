---
title: NetAdapterCx 限制
description: NetAdapterCx 限制
ms.assetid: 2333F2D9-A369-4124-9365-ABC49E8B5595
keywords:
- 网络适配器 WDF 类扩展限制，NetAdapterCx 限制，NetCx 限制
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21146fe5f8dc5301b1d2e07807f0328d69a9848d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375344"
---
# <a name="netadaptercx-limitations"></a>NetAdapterCx 限制

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

本主题介绍你应注意从 NetAdapterCx 客户端驱动程序调用 WDF 函数时需要注意的问题。

|函数 | 描述 |
|-|-|
| [**WdfDeviceInitAssignSDDLString**](https://msdn.microsoft.com/library/windows/hardware/ff546035) | 默认情况下[ **NetAdapterDeviceInitConfig** ](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)分配`SDDL_DEVOBJ_SYS_ALL_ADM_RWX_WORLD_RW_RES_R`作为默认 SDDL。 如果指定限制性更强的 SDDL，应用程序可能无法向适配器发送查询 Oid。 |
|[**WdfDeviceInitSetFileObjectConfig**](https://msdn.microsoft.com/library/windows/hardware/ff546107)| 不能设置客户端驱动程序**WdfFileObjectWdfCanUseFsContext**中**FileObjectClass**的成员[WDF_FILEOBJECT_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff551319)。 |
| [**WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)， [ **WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://msdn.microsoft.com/library/windows/hardware/hh706196)， [ **WdfDeviceInitSetDeviceType**](https://msdn.microsoft.com/library/windows/hardware/ff546090)， [ **WdfDeviceInitSetCharacteristics**](https://msdn.microsoft.com/library/windows/hardware/ff546074)， [ **WdfDeviceInitSetIoType**](https://msdn.microsoft.com/library/windows/hardware/ff546128)， [ **WdfDeviceInitSetPowerPageable**](https://msdn.microsoft.com/library/windows/hardware/ff546766) | [**NetAdapterDeviceInitConfig** ](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)代表客户端驱动程序调用这些例程。 客户端驱动程序不应调用它们。
| [**WdfDeviceCreateDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff545935) | 如果客户端驱动程序调用[ **WdfDeviceCreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff545935)与**ReferenceString**参数等于**NULL**，NDIS截获发送到设备接口的 I/O 请求。 若要避免此行为，指定引用的任何字符串。
