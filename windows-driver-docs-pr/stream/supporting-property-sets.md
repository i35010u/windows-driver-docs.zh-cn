---
title: 支持属性集
description: 支持属性集
ms.assetid: 49a3e3e6-3a09-4202-a2cb-df65806d3336
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，属性集
- 流式处理微型驱动程序 WDK Windows 2000 内核，属性集
- 微型驱动程序 WDK Windows 2000 内核流式处理，属性集
- 属性集 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 349a767367a6510be6a965f5ae2bb8b57dec605e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188337"
---
# <a name="supporting-property-sets"></a>支持属性集





这两个微型驱动程序均为整体，而单个流可以接收属性请求。 微型驱动程序提供其在[**HW \_ STREAM \_ 标头**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header)的**DevicePropertiesArray**中支持的属性集。 每个流都提供它在该流的[**HW \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)结构的**StreamPropertiesArray**中支持的属性集。

微型驱动程序定义了一个通过 [**KSPROPERTY \_ 集**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set) 数据结构处理的属性集，该结构将指向 [**KSPROPERTY \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item) 结构的数组，其中每个属性集中的一个属性。 如果 KSPROPERTY 项的 **GetSupported** 成员 \_ 为 **TRUE**，则微型驱动程序支持获取属性数据。 如果 KSPROPERTY 项的 **SetSupported** 成员 \_ 为 **TRUE**，则微型驱动程序支持设置属性数据。

大多数属性支持请求由类驱动程序自动处理，使用微型驱动程序在属性的 KSPROPERTY 项结构中提供的信息 \_ 。 例如，如果类驱动程序接收到 KSPROPERTY \_ 类型 \_ BASICSUPPORT 请求，它将在 KSPROPERTY 项的 **Values** 成员中查找数据类型和值范围 \_ 。 有关详细信息，请参阅 [**KSPROPERTY \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item) 。 如果微型驱动程序需要对支持请求执行自定义处理 (这种情况极少) ，则它可能会将 KSPROPERTY 项的 **SupportHandler** 成员设置 \_ 为 **TRUE**。 然后，类驱动程序处理该支持请求，就像它是属性 get 请求一样。 微型驱动程序可以从属性标识符的 **Flags** 成员确定请求的实际类型。

类驱动程序通过将 [**SRB \_ GET \_ 设备 \_ 属性**](./srb-get-device-property.md) 或 [**SRB \_ SET \_ 设备 \_ 属性**](./srb-set-device-property.md) 请求传递给微型驱动程序的 [*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb) 例程来获取或设置微型驱动程序属性。 类驱动程序通过将 SRB \_ GET \_ stream \_ 属性或 SRB \_ 设置 \_ 流 \_ 属性请求传递到流的 **StrMiniReceiveStreamControlPacket** 例程来获取或设置流属性。

类驱动程序代表微型驱动程序处理多个属性，并从微型驱动程序通过微型驱动程序的回调之一偶尔协助。 微型驱动程序不在其属性集数组中定义这些属性。 有关类驱动程序如何处理 [KSPROPSETID \_ Pin](./kspropsetid-pin.md) 和 [KSPROPSETID \_ 拓扑](./kspropsetid-topology.md) 属性集的说明，请参阅 [支持多个流](supporting-multiple-streams.md)。

 

