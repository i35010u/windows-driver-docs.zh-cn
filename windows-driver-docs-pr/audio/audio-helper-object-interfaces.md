---
title: 音频的帮助程序对象接口
description: 音频的帮助程序对象接口
ms.assetid: 94d3f7f3-7ccc-4f66-b5fa-95f18b8a0f17
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5a993a7dca6e1acf423b6870570416084e04bbf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533095"
---
# <a name="audio-helper-object-interfaces"></a>音频的帮助程序对象接口


## <span id="ddk_audio_helper_object_interfaces_ks"></span><span id="DDK_AUDIO_HELPER_OBJECT_INTERFACES_KS"></span>


端口 Class Library (portcls.sys) 实现多个提供的适配器驱动程序的常规使用的功能的帮助程序对象。 这些帮助程序对象提供用于管理 DMA 通道、 中断请求、 注册表访问、 资源列表中，数字版权和硬件事件的机制。 本部分提供这些对象公开的接口的详细信息。

此部分所述的以下接口：


[IDrmPort](https://msdn.microsoft.com/library/windows/hardware/ff536571)

可帮助跟踪的复合 DRM 权限的微型端口驱动程序。

[IDrmPort2](https://msdn.microsoft.com/library/windows/hardware/ff536573)

可帮助跟踪的复合 DRM 权限的微型端口驱动程序。 这是扩展的版本**IDrmPort**。

[IInterruptSync](https://msdn.microsoft.com/library/windows/hardware/ff536590)

同步机制来协调中断服务请求的共享的访问。

[IMasterClock](https://msdn.microsoft.com/library/windows/hardware/ff536696)

提供 DirectMusic 流具有访问权限当前引用时间从主时钟。

[**IPortClsEtwHelper**](https://msdn.microsoft.com/library/windows/hardware/dn265123)

微型端口驱动程序用于访问事件跟踪 Windows (ETW) 帮助器函数。
[IPortClsVersion](https://msdn.microsoft.com/library/windows/hardware/ff536877)

标识驱动程序上运行的 Microsoft Windows 操作系统版本。

[IPortEvents](https://msdn.microsoft.com/library/windows/hardware/ff536884)

由微型端口驱动程序来通知硬件事件的端口驱动程序。

[IPreFetchOffset](https://msdn.microsoft.com/library/windows/hardware/ff536951)

设置预提取偏移量，这是将写入光标从 play 光标 Microsoft DirectSound 硬件缓冲区中分离出来的数据的字节数。

[IRegistryKey](https://msdn.microsoft.com/library/windows/hardware/ff536965)

提供对注册表项及其子项的读/写访问。

[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)

指定 I/O 端口、 DMA 通道和中断等资源的列表。

[IServiceGroup](https://msdn.microsoft.com/library/windows/hardware/ff536994)

用于逐层到出现的对象列表的中断服务请求[IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)接口。

[IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)

表示中断服务请求的目标。

[IUnregisterPhysicalConnection](https://msdn.microsoft.com/library/windows/hardware/ff537022)

删除两个子设备相同的音频适配器中或在两个不同适配器之间的物理连接的注册。

[IUnregisterSubdevice](https://msdn.microsoft.com/library/windows/hardware/ff537030)

删除动态子音频适配器中的注册。

 

 





