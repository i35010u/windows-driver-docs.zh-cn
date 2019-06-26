---
title: 音频帮助程序对象接口
description: 音频帮助程序对象接口
ms.assetid: 94d3f7f3-7ccc-4f66-b5fa-95f18b8a0f17
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbd6a960d6932a30be10bb29eaf04262babd17c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355688"
---
# <a name="audio-helper-object-interfaces"></a>音频帮助程序对象接口


## <span id="ddk_audio_helper_object_interfaces_ks"></span><span id="DDK_AUDIO_HELPER_OBJECT_INTERFACES_KS"></span>


端口 Class Library (portcls.sys) 实现多个提供的适配器驱动程序的常规使用的功能的帮助程序对象。 这些帮助程序对象提供用于管理 DMA 通道、 中断请求、 注册表访问、 资源列表中，数字版权和硬件事件的机制。 本部分提供这些对象公开的接口的详细信息。

此部分所述的以下接口：


[IDrmPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idrmport)

可帮助跟踪的复合 DRM 权限的微型端口驱动程序。

[IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idrmport2)

可帮助跟踪的复合 DRM 权限的微型端口驱动程序。 这是扩展的版本**IDrmPort**。

[IInterruptSync](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iinterruptsync)

同步机制来协调中断服务请求的共享的访问。

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imasterclock)

提供 DirectMusic 流具有访问权限当前引用时间从主时钟。

[**IPortClsEtwHelper**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsetwhelper)

微型端口驱动程序用于访问事件跟踪 Windows (ETW) 帮助器函数。
[IPortClsVersion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsversion)

标识驱动程序上运行的 Microsoft Windows 操作系统版本。

[IPortEvents](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportevents)

由微型端口驱动程序来通知硬件事件的端口驱动程序。

[IPreFetchOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iprefetchoffset)

设置预提取偏移量，这是将写入光标从 play 光标 Microsoft DirectSound 硬件缓冲区中分离出来的数据的字节数。

[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iregistrykey)

提供对注册表项及其子项的读/写访问。

[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iresourcelist)

指定 I/O 端口、 DMA 通道和中断等资源的列表。

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)

用于逐层到出现的对象列表的中断服务请求[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)接口。

[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)

表示中断服务请求的目标。

[IUnregisterPhysicalConnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregisterphysicalconnection)

删除两个子设备相同的音频适配器中或在两个不同适配器之间的物理连接的注册。

[IUnregisterSubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregistersubdevice)

删除动态子音频适配器中的注册。

 

 





