---
title: 配置 BDA 筛选器
description: 配置 BDA 筛选器
ms.assetid: 4af9efc3-8073-4111-9ad0-8b2fba4d1545
keywords:
- 方法设置 WDK BDA，筛选器配置
- 属性设置 WDK BDA，筛选器配置
- KSMETHODSETID_BdaDeviceConfiguration
- 筛选器配置 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5676193716a52220377bff23cca7514b20369ef2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386644"
---
# <a name="configuring-a-bda-filter"></a>配置 BDA 筛选器





BDA 微型驱动程序处理的方法请求[KSMETHODSETID\_BdaDeviceConfiguration](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-bdadeviceconfiguration)方法设置为当前筛选器关系图中微型驱动程序中配置筛选器实例。

在以下代码片段中，两个方法的 KSMETHODSETID\_BdaDeviceConfiguration 方法集将被分派给 BDA 支持库的直接和剩余的方法先截获 BDA 微型驱动程序调度到之前BDA 支持库。

```cpp
//
//  BDA Device Configuration Method Set
//
//  Defines the dispatch routines for the filter level
//  topology configuration methods
//
DEFINE_KSMETHOD_TABLE(BdaDeviceConfigurationMethods)
{
    DEFINE_KSMETHOD_ITEM_BDA_CREATE_PIN_FACTORY(
        BdaMethodCreatePin,
        NULL
        ),
    DEFINE_KSMETHOD_ITEM_BDA_DELETE_PIN_FACTORY(
        BdaMethodDeletePin,
        NULL
        ),
    DEFINE_KSMETHOD_ITEM_BDA_CREATE_TOPOLOGY(
        CFilter::CreateTopology,
        NULL
        )
};
/*
** CreateTopology()
**
** Keeps track of topology association between input and output pins
**
*/
NTSTATUS
CFilter::
CreateTopology(
    IN PIRP         pIrp,
    IN PKSMETHOD    pKSMethod,
    PVOID           pvIgnored
    )
{
    NTSTATUS            Status = STATUS_SUCCESS;
    CFilter *           pFilter;
    ULONG               ulPinType;
    PKSFILTER           pKSFilter;

    ASSERT( pIrp);
    ASSERT( pKSMethod);

    //  Obtain a "this" pointer for the method.
    //
    //  Because this function is called directly from the property 
    //  dispatch table, get pointer to the underlying object.
    //
    pFilter = FilterFromIRP( pIrp);
    ASSERT( pFilter);
    if (!pFilter)
    {
        Status = STATUS_INVALID_PARAMETER;
        goto errExit;
    }

    //  Let the BDA support library create the standard topology.
    //  It will also validate the method, instance count, etc.
    //
    Status = BdaMethodCreateTopology( pIrp, pKSMethod, pvIgnored);
    if (Status != STATUS_SUCCESS)
    {
        goto errExit;
    }

    //  This is where the filter can keep track of associated pins.
    //
errExit:
    return Status;
}
```

KSMETHOD\_BDA\_创建\_拓扑方法请求调用微型驱动程序的 CFilter::CreateTopology 方法。 此方法调用 BDA 支持库函数[ **BdaMethodCreateTopology** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdamethodcreatetopology)创建筛选器插针之间的拓扑。 此函数在第 3 环，这反映了其他属性集，筛选器的已知的连接中实际创建拓扑结构。 BDA 微型驱动程序应截获 KSMETHOD\_BDA\_创建\_拓扑中所示上述代码段中如果该微型驱动程序时必须发送特殊说明硬件连接特定的方法请求pin 类型--例如，如果 BDA 设备执行硬件解多路复用，并创建任意数目的输出插针，按从单个输入插针关闭扇形展开。

 

 




