---
title: KSPROPSETID\_BdaPinControl
description: KSPROPSETID\_BdaPinControl
ms.assetid: f3c6ae83-d50f-49c8-a851-763f191f1932
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a141a911a42e6196b2196acaab2a714b4425b3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845628"
---
# <a name="kspropsetid_bdapincontrol"></a>KSPROPSETID\_BdaPinControl


## <span id="ddk_kspropsetid_bdapincontrol_ks"></span><span id="DDK_KSPROPSETID_BDAPINCONTROL_KS"></span>


KSPROPSETID\_BdaPinControl 为 BDA pin 控制属性集。 它用于检索有关特定 pin 的某些 BDA 特定的信息。

可用属性如下：

<span id="KSPROPERTY_BDA_PIN_ID"></span><span id="ksproperty_bda_pin_id"></span>[**KSPROPERTY\_BDA\_PIN\_ID**](ksproperty-bda-pin-id.md)  
返回 pin 的 BDA 标识符（ID）。

<span id="KSPROPERTY_BDA_PIN_TYPE"></span><span id="ksproperty_bda_pin_type"></span>[**KSPROPERTY\_BDA\_PIN\_类型**](ksproperty-bda-pin-type.md)  
返回指定 pin 类型的值。

### <a name="comments"></a>备注

在网络提供程序使用 KSMETHOD 创建用于筛选器的 pin 之后\_BDA\_创建\_\_工厂请求的 KSMETHODSETID\_BdaDeviceConfiguration 方法集，网络提供程序将使用属性KSPROPSETID\_BdaPinControl 更新其实际接收方拓扑的内部表示形式。

BDA 筛选器的每个 pin 工厂都应支持此属性集。 如果 BDA 微型驱动程序未定义此属性集，则在**BdaCreatePin**或**BdaInitFilter**函数创建 PIN 工厂时，bda 支持库将添加支持。

此属性集中的属性将返回有关 pin 的信息。 通常，不需要使用筛选器来截获其中的任何属性。 BDA 支持库提供了**BdaPropertyGetPinControl**默认函数来处理此属性集。

### <a name="see-also"></a>另请参阅

[**BdaCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacreatepin)、 [**BdaInitFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter)、 [**BdaPropertyGetPinControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertygetpincontrol)、 [KSMETHODSETID\_BdaDeviceConfiguration](ksmethodsetid-bdadeviceconfiguration.md)

 

 





