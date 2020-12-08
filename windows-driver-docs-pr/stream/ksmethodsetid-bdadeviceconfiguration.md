---
title: KSMETHODSETID \_ BdaDeviceConfiguration
description: KSMETHODSETID \_ BdaDeviceConfiguration
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee836b092c719a79a1f2e5683283ceae7164cf4b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788169"
---
# <a name="ksmethodsetid_bdadeviceconfiguration"></a>KSMETHODSETID \_ BdaDeviceConfiguration


## <span id="ddk_ksmethodsetid_bdadeviceconfiguration_ks"></span><span id="DDK_KSMETHODSETID_BDADEVICECONFIGURATION_KS"></span>


KSMETHODSETID \_ BdaDeviceConfiguration 是 BDA 设备配置方法集。 它用于配置筛选器关系图的筛选器。

有以下方法可用：

<span id="KSMETHOD_BDA_CREATE_PIN_FACTORY"></span><span id="ksmethod_bda_create_pin_factory"></span>[**KSMETHOD \_ BDA \_ 创建 \_ PIN \_ 工厂**](ksmethod-bda-create-pin-factory.md)  
触发为筛选器创建 pin 工厂的调用。

<span id="KSMETHOD_BDA_DELETE_PIN_FACTORY"></span><span id="ksmethod_bda_delete_pin_factory"></span>[**KSMETHOD \_ BDA \_ 删除 \_ PIN \_ 工厂**](ksmethod-bda-delete-pin-factory.md)  
触发删除筛选器的 pin 工厂的调用。

<span id="KSMETHOD_BDA_CREATE_TOPOLOGY"></span><span id="ksmethod_bda_create_topology"></span>[**KSMETHOD \_ BDA \_ CREATE \_ 拓扑**](ksmethod-bda-create-topology.md)  
在环3中创建一个反映筛选器中已知连接的拓扑结构。

### <a name="comments"></a>注释

此方法集是在筛选器上实现的。

如果 BDA 微型驱动程序未为此方法集中的方法定义自己的处理程序，则在 BDA 微型驱动程序调用 **BdaInitFilter** 函数时，bda 支持库将添加默认处理程序。

### <a name="see-also"></a>另请参阅

[**BdaInitFilter**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter)

 

