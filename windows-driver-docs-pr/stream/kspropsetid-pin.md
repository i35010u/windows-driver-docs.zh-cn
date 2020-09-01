---
title: KSPROPSETID \_ Pin
description: KSPROPSETID \_ Pin
ms.assetid: a74a9cb2-2809-4e03-95da-71eeb5f079e9
ms.date: 06/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: 18f8c643ed003556f0d76f69a3d72b9a7ff748bf
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185317"
---
# <a name="kspropsetid_pin"></a>KSPROPSETID \_ Pin


## <span id="ddk_kspropsetid_pin_ks"></span><span id="DDK_KSPROPSETID_PIN_KS"></span>


客户端使用 KSPROPSETID \_ 引脚属性集中的属性来查询 KS 筛选器，以获取有关它所支持的每个 Pin 工厂的信息。

[**KSPROPERTY \_ 引脚 \_ CTYPES**](ksproperty-pin-ctypes.md)属性指定 KS 筛选器支持多少个 PIN 工厂。 此属性集中的所有其他属性指定有关单个 pin 工厂的信息。 KS 筛选器按 ID （范围从零到 pin 工厂数减1）标识每个 pin 工厂。 客户端包括在颁发属性请求时所使用的 [**KSP \_ pin**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin) 结构内的 pin 工厂。

KSPROPSETID \_ 引脚属性集包括：

[**KSPROPERTY \_ PIN \_ 类别**](ksproperty-pin-category.md)

[**KSPROPERTY \_ PIN \_ CINSTANCES**](ksproperty-pin-cinstances.md)

[**KSPROPERTY \_ PIN \_ 通信**](ksproperty-pin-communication.md)

[**KSPROPERTY \_ PIN \_ CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

[**KSPROPERTY \_ PIN \_ CTYPES**](ksproperty-pin-ctypes.md)

[**KSPROPERTY \_ PIN \_ 数据流**](ksproperty-pin-dataflow.md)

[**KSPROPERTY \_ PIN \_ DATAINTERSECTION**](ksproperty-pin-dataintersection.md)

[**KSPROPERTY \_ PIN \_ DATARANGES**](ksproperty-pin-dataranges.md)

[**KSPROPERTY \_ PIN \_ GLOBALCINSTANCES**](ksproperty-pin-globalcinstances.md)

[**KSPROPERTY \_ PIN \_ 接口**](ksproperty-pin-interfaces.md)

[**KSPROPERTY \_ PIN \_ 媒体**](ksproperty-pin-mediums.md)

[**KSPROPERTY \_ PIN \_ MODEDATAFORMATS**](ksproperty-pin-modedataformats.md)

[**KSPROPERTY \_ PIN \_ 名称**](ksproperty-pin-name.md)

[**KSPROPERTY \_ PIN \_ NECESSARYINSTANCES**](ksproperty-pin-necessaryinstances.md)

[**KSPROPERTY \_ PIN \_ PHYSICALCONNECTION**](ksproperty-pin-physicalconnection.md)

[**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

[**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2**](ksproperty-pin-proposedataformat2.md)

 

