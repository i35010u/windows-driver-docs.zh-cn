---
title: KS 属性、 事件和方法
description: KS 属性、 事件和方法
ms.assetid: 933bbe81-92d8-4bcc-b935-9ae929464ca1
keywords:
- 内核流式处理 WDK，属性
- KS 属性 WDK 内核流式处理
- 流式处理 WDK，事件的内核
- KS WDK 事件
- 流式处理 WDK，方法的内核
- KS WDK 方法
- 流式处理的属性 WDK 内核
- 流式处理事件 WDK 内核
- 流式处理的方法 WDK 内核
- 别名结构 WDK 内核流式处理
- 设置操作 WDK 内核的流式处理
- 获取操作 WDK 内核的流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be71c7dd505e9376bbd18199b8a012a3c35a89d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521843"
---
# <a name="ks-properties-events-and-methods"></a>KS 属性、 事件和方法





流式处理体系结构的内核支持通过微型驱动程序和用户模式下客户端之间的交互[属性](ks-properties.md)，[事件](ks-events.md)，并[方法](ks-methods.md)。 使用这些构造，KS 对象的客户端可以获取和设置对象状态、 注册通知回调的事件，并执行对象的方法。

客户端以标准化方式请求所有三个操作类。 客户端提供的别名结构[ **KSIDENTIFIER** ](https://msdn.microsoft.com/library/windows/hardware/ff562676)对的调用中**DeviceIoControl** （Microsoft Windows SDK 文档中所述） 或[**KsSynchronousDeviceControl**](https://msdn.microsoft.com/library/windows/hardware/ff567142)。

别名结构是否[ **KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)， [ **KSEVENT**](https://msdn.microsoft.com/library/windows/hardware/ff561744)，并[ **KSMETHOD**](https://msdn.microsoft.com/library/windows/hardware/ff563398). 所有这三个包含以下参数：

-   **Set**

    在一组中，在功能上类似的操作组合在一起。 每个属性、 事件或方法集是由 GUID 标识。 Microsoft 为标准的特定于技术的操作定义 Guid。 微型驱动程序可以定义其自己的自定义操作的 Guid。

-   **标识符**

    每个操作被指定的集内的 ID 号。

-   **特定于操作的标识数据**

    某些属性请求要求提供附加数据。 例如，音频设备支持上的插针[KSPROPSETID\_音频](https://msdn.microsoft.com/library/windows/hardware/ff537440)属性集。 音频接口可能支持多个不同的音频声道。 客户端获取或设置某些 KSPROPSETID\_音频属性必须指定请求应用的音频通道。 事件和方法的请求不需要额外的数据。

Microsoft 定义集 Guid 和标识符的多用途操作标头中的位置*ks.h*。 在中找到标准 Guid 和多媒体技术的特定类的标识符*ksmedia.h*。

AVStream 微型驱动程序支持属性、 事件和方法，通过提供一个指向[ **KSAUTOMATION\_表**](https://msdn.microsoft.com/library/windows/hardware/ff560990)中的相关结构[ **KSFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff562553)或[ **KSPIN\_描述符\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534)。 KSAUTOMATION\_表包含指向的数组的指针[ **KSPROPERTY\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff565617)对象。 若要了解详细信息，请参阅[定义自动化表](defining-automation-tables.md)。

以下各节包含有关如何微型驱动程序支持的三个操作类的信息：

[KS 属性](ks-properties.md)

[KS 事件](ks-events.md)

[KS 方法](ks-methods.md)

 

 




