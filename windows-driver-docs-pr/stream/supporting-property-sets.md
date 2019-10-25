---
title: 支持属性集
description: 支持属性集
ms.assetid: 49a3e3e6-3a09-4202-a2cb-df65806d3336
keywords:
- Stream .sys 类驱动程序 WDK Windows 2000 内核，属性集
- 流式处理微型驱动程序 WDK Windows 2000 内核，属性集
- 微型驱动程序 WDK Windows 2000 内核流式处理，属性集
- 属性集 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb985211af2c8c20ff484f5f5b78ebe9c58db215
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837664"
---
# <a name="supporting-property-sets"></a>支持属性集





这两个微型驱动程序均为整体，而单个流可以接收属性请求。 微型驱动程序提供其在 DevicePropertiesArray [ **\_STREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header)的中支持的属性集。 每个流都提供它在**StreamPropertiesArray**中支持的属性集， [ **\_流的\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)结构。

微型驱动程序定义了一个通过[**KSPROPERTY\_集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)数据结构来处理的属性集，该结构依次指向[**KSPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)结构的数组，其中每个属性都对应于属性集中的一个属性。 如果 KSPROPERTY 的**GetSupported**成员\_项为**TRUE**，则微型驱动程序支持获取属性数据。 如果 KSPROPERTY 的**SetSupported**成员\_项为**TRUE**，则微型驱动程序支持设置属性数据。

大多数属性支持请求由类驱动程序自动处理，使用微型驱动程序在属性的 KSPROPERTY\_项结构中提供的信息。 例如，如果类驱动程序接收到 KSPROPERTY\_类型\_BASICSUPPORT 请求，它将在 KSPROPERTY\_项的**Values**成员中查找数据类型和值范围。 有关详细信息，请参阅[**KSPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)。 如果微型驱动程序需要执行对支持请求的自定义处理（这种情况很少见），则它可能会将 KSPROPERTY\_项的**SupportHandler**成员设置为**TRUE**。 然后，类驱动程序处理该支持请求，就像它是属性 get 请求一样。 微型驱动程序可以从属性标识符的**Flags**成员确定请求的实际类型。

类驱动程序通过传递 SRB\_获取或设置微型驱动程序属性， [ **\_设备\_属性**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-device-property)或[**SRB\_将\_设备\_属性请求设置**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-device-property)为微型驱动程序的[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)例程。 类驱动程序获取或设置流属性，方法是传递 SRB\_获取\_STREAM\_属性或 SRB\_将\_STREAM\_属性请求设置为流的**StrMiniReceiveStreamControlPacket**例程。

类驱动程序代表微型驱动程序处理多个属性，并从微型驱动程序通过微型驱动程序的回调之一偶尔协助。 微型驱动程序不在其属性集数组中定义这些属性。 有关类驱动程序如何处理[KSPROPSETID\_固定](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)和[KSPROPSETID\_拓扑](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)属性集的说明，请参阅[支持多个流](supporting-multiple-streams.md)。

 

 




