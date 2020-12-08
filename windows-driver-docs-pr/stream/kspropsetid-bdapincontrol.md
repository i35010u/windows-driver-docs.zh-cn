---
title: KSPROPSETID \_ BdaPinControl
description: KSPROPSETID \_ BdaPinControl
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a923f866a0d6471b3a01a577756f453a957f78c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837835"
---
# <a name="kspropsetid_bdapincontrol"></a>KSPROPSETID \_ BdaPinControl


## <span id="ddk_kspropsetid_bdapincontrol_ks"></span><span id="DDK_KSPROPSETID_BDAPINCONTROL_KS"></span>


KSPROPSETID \_ BdaPinControl 是 BDA pin 控制属性集。 它用于检索有关特定 pin 的某些 BDA 特定的信息。

以下属性可用：

<span id="KSPROPERTY_BDA_PIN_ID"></span><span id="ksproperty_bda_pin_id"></span>[**KSPROPERTY \_ BDA \_ PIN \_ ID**](ksproperty-bda-pin-id.md)  
返回 pin)  (ID 的 BDA 标识符。

<span id="KSPROPERTY_BDA_PIN_TYPE"></span><span id="ksproperty_bda_pin_type"></span>[**KSPROPERTY \_ BDA \_ PIN \_ 类型**](ksproperty-bda-pin-type.md)  
返回指定 pin 类型的值。

### <a name="comments"></a>注释

使用 KSMETHOD \_ BDA \_ CREATE \_ PIN \_ 工厂请求 KSMETHODSETID BdaDeviceConfiguration 方法集为筛选器创建 pin 后 \_ ，网络提供程序将使用 KSPROPSETID BdaPinControl 的属性 \_ 来更新其实际接收方拓扑的内部表示形式。

BDA 筛选器的每个 pin 工厂都应支持此属性集。 如果 BDA 微型驱动程序未定义此属性集，则在 **BdaCreatePin** 或 **BdaInitFilter** 函数创建 PIN 工厂时，bda 支持库将添加支持。

此属性集中的属性将返回有关 pin 的信息。 通常，不需要使用筛选器来截获其中的任何属性。 BDA 支持库提供了 **BdaPropertyGetPinControl** 默认函数来处理此属性集。

### <a name="see-also"></a>另请参阅

[**BdaCreatePin**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacreatepin)、 [**BdaInitFilter**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter)、 [**BdaPropertyGetPinControl**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertygetpincontrol)、 [KSMETHODSETID \_ BdaDeviceConfiguration](ksmethodsetid-bdadeviceconfiguration.md)

 

