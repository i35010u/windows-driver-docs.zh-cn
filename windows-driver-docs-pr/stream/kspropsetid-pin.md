---
title: KSPROPSETID\_Pin
description: KSPROPSETID\_Pin
ms.assetid: a74a9cb2-2809-4e03-95da-71eeb5f079e9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ead0a61a66c47591e757b97d57010aedc869f706
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845625"
---
# <a name="kspropsetid_pin"></a>KSPROPSETID\_Pin


## <span id="ddk_kspropsetid_pin_ks"></span><span id="DDK_KSPROPSETID_PIN_KS"></span>


客户端使用 KSPROPSETID\_固定属性集中的属性来查询 KS 筛选器，以获取有关它所支持的每个 Pin 工厂的信息。

[**KSPROPERTY\_引脚\_CTYPES**](ksproperty-pin-ctypes.md)属性指定 KS 筛选器支持多少个 PIN 工厂。 此属性集中的所有其他属性指定有关单个 pin 工厂的信息。 KS 筛选器按 ID （范围从零到 pin 工厂数减1）标识每个 pin 工厂。 客户端在[**KSP\_pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)结构中包括 Pin 工厂 T，此端口在发出属性请求时使用。

KSPROPSETID\_引脚属性集包括：

[**KSPROPERTY\_固定\_类别**](ksproperty-pin-category.md)

[**KSPROPERTY\_PIN\_CINSTANCES**](ksproperty-pin-cinstances.md)

[**KSPROPERTY\_PIN\_通信**](ksproperty-pin-communication.md)

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

[**KSPROPERTY\_PIN\_CTYPES**](ksproperty-pin-ctypes.md)

[**KSPROPERTY\_PIN\_数据流**](ksproperty-pin-dataflow.md)

[**KSPROPERTY\_PIN\_DATAINTERSECTION**](ksproperty-pin-dataintersection.md)

[**KSPROPERTY\_PIN\_DATARANGES**](ksproperty-pin-dataranges.md)

[**KSPROPERTY\_PIN\_GLOBALCINSTANCES**](ksproperty-pin-globalcinstances.md)

[**KSPROPERTY\_固定\_接口**](ksproperty-pin-interfaces.md)

[**KSPROPERTY\_固定\_媒介**](ksproperty-pin-mediums.md)

[**KSPROPERTY\_PIN\_名称**](ksproperty-pin-name.md)

[**KSPROPERTY\_PIN\_NECESSARYINSTANCES**](ksproperty-pin-necessaryinstances.md)

[**KSPROPERTY\_PIN\_PHYSICALCONNECTION**](ksproperty-pin-physicalconnection.md)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**](ksproperty-pin-proposedataformat2.md)

 

 





