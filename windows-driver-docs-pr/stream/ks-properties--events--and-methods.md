---
title: KS 属性、事件和方法
description: KS 属性、事件和方法
ms.assetid: 933bbe81-92d8-4bcc-b935-9ae929464ca1
keywords:
- 内核流 WDK，属性
- KS 属性 WDK 内核流式处理
- 内核流 WDK，事件
- KS WDK，事件
- 内核流 WDK，方法
- KS WDK，方法
- 属性 WDK 内核流式处理
- 事件 WDK 内核流式处理
- 方法 WDK 内核流式处理
- 别名结构 WDK 内核流式处理
- 设置操作 WDK 内核流式处理
- 获取操作 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ca8c41beb16133204e70251b1fe0d46479736f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842509"
---
# <a name="ks-properties-events-and-methods"></a>KS 属性、事件和方法





内核流式处理体系结构支持通过[属性](ks-properties.md)、[事件](ks-events.md)和[方法](ks-methods.md)在微型驱动程序与用户模式客户端之间进行交互。 使用这些构造，KS 对象的客户端可以获取和设置对象状态、注册事件的通知回调和执行对象方法。

客户端以标准化的方式请求所有三个操作类。 在对**DeviceIoControl**的调用中，客户端提供[**KSIDENTIFIER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)的别名结构（如 Microsoft Windows SDK 文档中所述）或[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)。

别名结构包括[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)、 [**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))和[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))。 所有三个包含以下参数：

-   **字符集**

    功能类似的操作在集中组合在一起。 每个属性、事件或方法集均由 GUID 标识。 Microsoft 为标准技术特定操作定义了 Guid。 微型驱动程序可以为自定义操作定义自己的 Guid。

-   **Identifier**

    每个操作由该集内的一个 ID 号来指定。

-   **特定于操作的标识数据**

    某些属性请求需要额外的数据。 例如，音频设备上的 pin 支持[KSPROPSETID\_音频](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audio)属性集。 音频 pin 可能支持多种不同的音频通道。 获取或设置某些 KSPROPSETID\_音频属性的客户端必须指定请求适用的音频通道。 事件和方法请求不需要其他数据。

用于常规用途操作的 Microsoft 定义的设置 Guid 和标识符位于标头*ks*中。 *Ksmedia*中提供了适用于多媒体技术的特定类的标准 guid 和标识符。

AVStream 微型驱动程序支持属性、事件和方法，方法是：在相关[**KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)中提供一个指向[**KSAUTOMATION\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksautomation_table_)结构的指针，或在[ **\_EX 中提供 KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)。 KSAUTOMATION\_表包含指向[**KSPROPERTY\_集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)对象的数组的指针。 若要了解详细信息，请参阅[定义自动化表](defining-automation-tables.md)。

以下部分包含有关微型驱动程序如何支持这三个操作类的信息：

[KS 属性](ks-properties.md)

[KS 事件](ks-events.md)

[KS 方法](ks-methods.md)

 

 




