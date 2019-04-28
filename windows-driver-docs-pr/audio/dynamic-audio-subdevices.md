---
title: 动态音频子设备
description: 动态音频子设备
ms.assetid: d8ebd6d9-37ed-4890-aae1-5ecf58f2e22a
keywords:
- WDM 音频驱动程序 WDK，动态子设备
- 音频驱动程序 WDK，动态子设备
- 动态子音频设备 WDK 音频
- 子设备 WDK 音频
- 音频编解码器 WDK
- jack 存在检测 WDK 音频
- 删除子设备
- 删除子设备
- 正在注销子设备
- 动态子设备 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d62eeae42a398208407d120df7be4a193041728f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333727"
---
# <a name="dynamic-audio-subdevices"></a>动态音频子设备


某些音频适配器可以在运行时动态更改其内部的拓扑。 通过在 PortCls 系统驱动程序 (Portcls.sys) 中使用的系统提供的功能，适配器驱动程序可以提供可动态配置的音频硬件的软件的支持。

例如， [Intel 高定义音频规范](https://go.microsoft.com/fwlink/p/?linkid=42508)使用的术语音频编解码器来指代集成音频适配器连接到通过 HD 音频链接界面的高清晰度音频 (HD Audio) 控制器。 典型的音频编解码器支持 jack 在场检测： 硬件即插即用是插入或删除时从一个插孔，生成中断通知在硬件配置中更改的驱动程序。 例如，驱动程序插入到耳机插孔的即插即用的响应创建[KS 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff567644)来表示耳机音频子。 该驱动程序将硬件资源分配给筛选器 （例如，耳机可能要求的音量控件和数字模拟转换器或 DAC） 并将该筛选器注册为音频设备。 当用户断开耳机时，驱动程序通过释放资源，正在删除筛选器，并从注册表中删除该响应。

此行为可确保当音频应用程序检查以查看哪些音频设备注册时，找到目前处于插入状态的设备。 如果设备被拔出，它不在注册表中。

在 Windows Vista、 Windows Server 2003 Service Pack 1 (SP1) 和 Windows XP Service Pack 2 (SP2)，支持 PortCls [IUnregisterSubdevice](https://msdn.microsoft.com/library/windows/hardware/ff537030)并[IUnregisterPhysicalConnection](https://msdn.microsoft.com/library/windows/hardware/ff537022)接口。 音频适配器驱动程序使用这两个接口删除不再使用的音频子设备。 早期版本的 Windows，包括 Windows Server 2003 和 Windows XP 不支持这些接口。 在这些早期版本的 Windows 中，子设备可以是创建但未删除--一旦创建子，它存在适配器驱动程序对象的生存期内。

**IUnregisterSubdevice**接口包含一个方法，该适配器驱动程序可以使用"注销"驱动程序已注册通过以前调用子[ **PcRegisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537731)例程：

[**IUnregisterSubdevice::UnregisterSubdevice**](https://msdn.microsoft.com/library/windows/hardware/ff537032)

**IUnregisterPhysicalConnection**接口包含三个适配器驱动程序可用于取消注册子设备之间的物理连接的方法：

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnection**](https://msdn.microsoft.com/library/windows/hardware/ff537024)

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnectionFromExternal**](https://msdn.microsoft.com/library/windows/hardware/ff537027)

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnectionToExternal**](https://msdn.microsoft.com/library/windows/hardware/ff537029)

这些方法可删除通过以前调用注册的驱动程序的连接[ **PcRegisterPhysicalConnection**](https://msdn.microsoft.com/library/windows/hardware/ff537726)， [ **PcRegisterPhysicalConnectionFromExternal**](https://msdn.microsoft.com/library/windows/hardware/ff537728)，并[ **PcRegisterPhysicalConnectionToExternal** ](https://msdn.microsoft.com/library/windows/hardware/ff537729)例程。 将从 PcRegisterPhysicalConnection 信息存储在 PortCls*Xxx*调用，以便端口驱动程序随后可以使用的信息来响应[ **KSPROPERTY\_PIN\_PHYSICALCONNECTION** ](https://msdn.microsoft.com/library/windows/hardware/ff565205)属性请求。 在删除子从适配器的拓扑时，该驱动程序必须取消注册子的物理连接到拓扑的该部分。 若要取消注册子的物理连接可能导致内存泄漏。 PortCls 支持 PcRegister*Xxx*例程在 Windows 2000 及更高版本和 Windows Me / 98。

在本部分中的以下主题介绍如何实现具有动态拓扑的适配器的驱动程序支持：

[管理动态拓扑](managing-dynamic-topologies.md)

[针对动态子设备驱动程序支持](driver-support-for-dynamic-subdevices.md)

[Jack 动态子音频设备的说明](jack-descriptions-for-dynamic-audio-subdevices.md)

 

 




