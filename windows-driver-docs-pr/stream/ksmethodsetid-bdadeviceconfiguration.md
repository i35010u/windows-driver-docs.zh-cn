---
title: KSMETHODSETID\_BdaDeviceConfiguration
description: KSMETHODSETID\_BdaDeviceConfiguration
ms.assetid: a0014869-2ea0-4f55-be3a-da1e624ad61c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1b44ce62c6503a8e9c167d4abb47a08c143d97b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842415"
---
# <a name="ksmethodsetid_bdadeviceconfiguration"></a>KSMETHODSETID\_BdaDeviceConfiguration


## <span id="ddk_ksmethodsetid_bdadeviceconfiguration_ks"></span><span id="DDK_KSMETHODSETID_BDADEVICECONFIGURATION_KS"></span>


KSMETHODSETID\_BdaDeviceConfiguration 为 BDA 设备配置方法集。 它用于配置筛选器关系图的筛选器。

可采用以下方法：

<span id="KSMETHOD_BDA_CREATE_PIN_FACTORY"></span><span id="ksmethod_bda_create_pin_factory"></span>[**KSMETHOD\_BDA\_创建\_PIN\_工厂**](ksmethod-bda-create-pin-factory.md)  
触发为筛选器创建 pin 工厂的调用。

<span id="KSMETHOD_BDA_DELETE_PIN_FACTORY"></span><span id="ksmethod_bda_delete_pin_factory"></span>[**KSMETHOD\_BDA\_删除\_PIN\_工厂**](ksmethod-bda-delete-pin-factory.md)  
触发删除筛选器的 pin 工厂的调用。

<span id="KSMETHOD_BDA_CREATE_TOPOLOGY"></span><span id="ksmethod_bda_create_topology"></span>[**KSMETHOD\_BDA\_创建\_拓扑**](ksmethod-bda-create-topology.md)  
在环3中创建一个反映筛选器中已知连接的拓扑结构。

### <a name="comments"></a>备注

此方法集是在筛选器上实现的。

如果 BDA 微型驱动程序未为此方法集中的方法定义自己的处理程序，则在 BDA 微型驱动程序调用**BdaInitFilter**函数时，bda 支持库将添加默认处理程序。

### <a name="see-also"></a>另请参阅

[**BdaInitFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter)

 

 





