---
title: KSMETHODSETID\_BdaDeviceConfiguration
description: KSMETHODSETID\_BdaDeviceConfiguration
ms.assetid: a0014869-2ea0-4f55-be3a-da1e624ad61c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f1f54f083881bc8dc856ce2a2909240b33aea99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362631"
---
# <a name="ksmethodsetidbdadeviceconfiguration"></a>KSMETHODSETID\_BdaDeviceConfiguration


## <span id="ddk_ksmethodsetid_bdadeviceconfiguration_ks"></span><span id="DDK_KSMETHODSETID_BDADEVICECONFIGURATION_KS"></span>


KSMETHODSETID\_BdaDeviceConfiguration 是 BDA 设备配置方法集。 它用于配置的筛选器图形的筛选器。

可采用以下方法：

<span id="KSMETHOD_BDA_CREATE_PIN_FACTORY"></span><span id="ksmethod_bda_create_pin_factory"></span>[**KSMETHOD\_BDA\_创建\_PIN\_工厂**](ksmethod-bda-create-pin-factory.md)  
触发创建 pin 的筛选器的调用。

<span id="KSMETHOD_BDA_DELETE_PIN_FACTORY"></span><span id="ksmethod_bda_delete_pin_factory"></span>[**KSMETHOD\_BDA\_删除\_PIN\_工厂**](ksmethod-bda-delete-pin-factory.md)  
触发删除筛选器的 pin 工厂的调用。

<span id="KSMETHOD_BDA_CREATE_TOPOLOGY"></span><span id="ksmethod_bda_create_topology"></span>[**KSMETHOD\_BDA\_创建\_拓扑**](ksmethod-bda-create-topology.md)  
在将反映在筛选器中的已知的连接的 3 环中创建的拓扑结构。

### <a name="comments"></a>备注

此方法集是对筛选器实现的。

如果 BDA 微型驱动程序不会定义是自己的处理程序方法中设置此方法，则 BDA 支持库将添加默认处理程序，当 BDA 微型驱动程序调用**BdaInitFilter**函数。

### <a name="see-also"></a>请参阅

[**BdaInitFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdainitfilter)

 

 





