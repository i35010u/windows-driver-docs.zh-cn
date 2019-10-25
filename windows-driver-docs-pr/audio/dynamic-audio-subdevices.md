---
title: 动态音频子设备
description: 动态音频子设备
ms.assetid: d8ebd6d9-37ed-4890-aae1-5ecf58f2e22a
keywords:
- WDM 音频驱动程序 WDK，动态 subdevices
- 音频驱动程序 WDK，动态 subdevices
- 动态音频 subdevices WDK 音频
- subdevices WDK 音频
- 音频编解码器 WDK
- 插座状态检测 WDK 音频
- 删除 subdevices
- 删除 subdevices
- 正在取消注册 subdevices
- 动态 subdevices WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73b038ccfd4f2bb4ef9fc6331d5905771305d8b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831257"
---
# <a name="dynamic-audio-subdevices"></a>动态音频子设备


某些音频适配器可在运行时动态更改其内部拓扑。 通过使用 PortCls 系统驱动程序（Portcls）中系统提供的功能，适配器驱动程序可以为动态配置的音频硬件提供软件支持。

例如， [Intel 高质音频规范](https://go.microsoft.com/fwlink/p/?linkid=42508)使用术语 "音频编解码器" 引用通过高清音频链接接口连接到高清晰音频（HD 音频）控制器的集成音频适配器。 典型的音频编解码器支持插孔状态检测：当插入插座或从插孔中删除插件时，硬件将生成一个中断以通知驱动程序硬件配置中的更改。 例如，驱动程序通过创建用于表示耳机音频 subdevice 的[KS 筛选器](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-filters)来响应插入耳机插孔的插入。 驱动程序将硬件资源分配给筛选器（例如，耳机可能需要使用音量控制和数字到模拟转换器或 DAC），并将筛选器注册为音频设备。 当用户断开耳机时，驱动程序将通过释放资源、删除筛选器并从注册表中删除来做出响应。

此行为可确保当音频应用程序检查哪些音频设备已注册时，它仅查找当前插入的设备。 如果设备已拔出，则它不会显示在注册表中。

在 Windows Vista 中，Windows Server 2003 Service Pack 1 （SP1）和 Windows XP Service Pack 2 （SP2），PortCls 支持[IUnregisterSubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregistersubdevice)和[IUnregisterPhysicalConnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregisterphysicalconnection)接口。 音频适配器驱动程序使用这两个接口删除不再使用的音频 subdevices。 Windows 的早期版本（包括 Windows Server 2003 和 Windows XP）不支持这些接口。 在这些早期版本的 Windows 中，可以创建但不删除 subdevices--一旦创建了 subdevice，就会在适配器驱动程序对象的生存期内使用它。

**IUnregisterSubdevice**接口包含单一方法，适配器驱动程序可以使用该方法 "取消注册" subdevice，驱动程序通过之前对[**PcRegisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)例程的调用注册了该驱动程序：

[**IUnregisterSubdevice::UnregisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice)

**IUnregisterPhysicalConnection**接口包含三种方法，适配器驱动程序可以使用这些方法注销 subdevices 之间的物理连接：

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnection)

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnectionFromExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnectionfromexternal)

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnectionToExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnectiontoexternal)

这些方法删除了驱动程序通过先前对[**PcRegisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)、 [**PcRegisterPhysicalConnectionFromExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal)和[**PcRegisterPhysicalConnectionToExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal)例程的调用注册的连接。 PortCls 存储 PcRegisterPhysicalConnection*Xxx*调用中的信息，以便端口驱动程序随后可以使用该信息对[**KSPROPERTY\_PIN\_PHYSICALCONNECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-physicalconnection)属性请求进行响应。 从适配器的拓扑中删除 subdevice 时，驱动程序必须将 subdevice 的物理连接取消注册到拓扑的该部分。 未能注销 subdevice 的物理连接可能会导致内存泄漏。 PortCls 支持 Windows 2000 和更高版本以及 Windows Me/98 中的 PcRegister*Xxx*例程。

本节中的以下主题介绍如何为具有动态拓扑的适配器实现驱动程序支持：

[管理动态拓扑](managing-dynamic-topologies.md)

[动态 Subdevices 的驱动程序支持](driver-support-for-dynamic-subdevices.md)

[动态音频 Subdevices 的插孔说明](jack-descriptions-for-dynamic-audio-subdevices.md)

 

 




