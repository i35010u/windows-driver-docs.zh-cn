---
title: 音频帮助程序对象接口
description: 音频帮助程序对象接口
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 703db3a5fbc268e9cafb17b071aca3944662eba1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784975"
---
# <a name="audio-helper-object-interfaces"></a>音频帮助程序对象接口


## <span id="ddk_audio_helper_object_interfaces_ks"></span><span id="DDK_AUDIO_HELPER_OBJECT_INTERFACES_KS"></span>


端口类库 ( # A0) 实现了各种帮助器对象，这些对象提供对适配器驱动程序通用的功能。 这些帮助对象提供管理 DMA 通道、中断请求、注册表访问、资源列表、数字权限和硬件事件的机制。 本部分提供有关这些对象公开的接口的详细信息。

本部分介绍以下接口：


[IDrmPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport)

帮助微型端口驱动程序跟踪复合 DRM 权限。

[IDrmPort2](/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport2)

帮助微型端口驱动程序跟踪复合 DRM 权限。 这是 **IDrmPort** 的扩展版本。

[IInterruptSync](/windows-hardware/drivers/ddi/portcls/nn-portcls-iinterruptsync)

用于协调对中断服务请求的共享访问的同步机制。

[IMasterClock](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)

向 DirectMusic 流提供对主时钟的当前引用时间的访问。

[**IPortClsEtwHelper**](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsetwhelper)

由微型端口驱动程序用来访问 Windows (ETW) helper 函数的事件跟踪。
[IPortClsVersion](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsversion)

标识运行驱动程序的 Microsoft Windows 操作系统的版本。

[IPortEvents](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportevents)

由微型端口驱动程序用来通知硬件事件的端口驱动程序。

[IPreFetchOffset](/windows-hardware/drivers/ddi/portcls/nn-portcls-iprefetchoffset)

设置预提取偏移量，它是在 Microsoft DirectSound 硬件缓冲区中将写入游标与播放光标分隔的数据字节数。

[IRegistryKey](/windows-hardware/drivers/ddi/portcls/nn-portcls-iregistrykey)

提供对注册表项及其子项的读/写访问权限。

[IResourceList](/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)

指定 i/o 端口、DMA 通道和中断等资源的列表。

[IServiceGroup](/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)

用于通过 [IServiceSink](/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink) 接口将中断服务请求 demultiplex 到对象列表。

[IServiceSink](/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)

表示中断服务请求的目标。

[IUnregisterPhysicalConnection](/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregisterphysicalconnection)

删除同一音频适配器或两个不同适配器中两个 subdevices 之间的物理连接的注册。

[IUnregisterSubdevice](/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregistersubdevice)

删除音频适配器中动态 subdevice 的注册。

 

