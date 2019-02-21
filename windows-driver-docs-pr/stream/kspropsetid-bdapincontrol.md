---
title: KSPROPSETID\_BdaPinControl
description: KSPROPSETID\_BdaPinControl
ms.assetid: f3c6ae83-d50f-49c8-a851-763f191f1932
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8c7d765eef00b29bc36c20fb68337b9d90104d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523555"
---
# <a name="kspropsetidbdapincontrol"></a>KSPROPSETID\_BdaPinControl


## <span id="ddk_kspropsetid_bdapincontrol_ks"></span><span id="DDK_KSPROPSETID_BDAPINCONTROL_KS"></span>


KSPROPSETID\_BdaPinControl 是 BDA pin 控件属性集。 它用于检索有关特定 pin 一些 BDA 特定的信息。

可用属性如下：

<span id="KSPROPERTY_BDA_PIN_ID"></span><span id="ksproperty_bda_pin_id"></span>[**KSPROPERTY\_BDA\_PIN\_ID**](ksproperty-bda-pin-id.md)  
返回 pin 的 BDA 标识符 (ID)。

<span id="KSPROPERTY_BDA_PIN_TYPE"></span><span id="ksproperty_bda_pin_type"></span>[**KSPROPERTY\_BDA\_PIN\_TYPE**](ksproperty-bda-pin-type.md)  
返回指定的 pin 的类型的值。

### <a name="comments"></a>备注

完成后网络提供程序创建筛选器使用 KSMETHOD pin\_BDA\_创建\_PIN\_工厂请求的 KSMETHODSETID\_BdaDeviceConfiguration 方法集，网络提供商将使用 KSPROPSETID 属性\_BdaPinControl 更新实际接收方拓扑其内部表示形式。

BDA 筛选器的每个 pin 工厂应支持设置此属性。 如果 BDA 微型驱动程序未定义此属性集，则 BDA 支持库添加了支持通过以下任一方法创建 pin 工厂时**BdaCreatePin**或**BdaInitFilter**函数。

此属性中的属性设置旋转中心点返回的信息。 通常情况下，筛选器的 pin 不需要截获任何这些属性。 BDA 支持库提供了**BdaPropertyGetPinControl**默认函数来处理此属性组。

### <a name="see-also"></a>另请参阅

[**BdaCreatePin**](https://msdn.microsoft.com/library/windows/hardware/ff556445)， [ **BdaInitFilter**](https://msdn.microsoft.com/library/windows/hardware/ff556464)， [ **BdaPropertyGetPinControl**](https://msdn.microsoft.com/library/windows/hardware/ff556483)， [KSMETHODSETID\_BdaDeviceConfiguration](ksmethodsetid-bdadeviceconfiguration.md)

 

 





