---
title: 配置 BDA 筛选器
description: 配置 BDA 筛选器
ms.assetid: 4af9efc3-8073-4111-9ad0-8b2fba4d1545
keywords:
- 方法设置 WDK BDA，筛选器配置
- 属性设置 WDK BDA，筛选器配置
- KSMETHODSETID_BdaDeviceConfiguration
- 筛选配置 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296d4878606675847f62db3cbbfbaabebf9c1b71
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191821"
---
# <a name="configuring-a-bda-filter"></a>配置 BDA 筛选器





BDA 微型驱动程序处理 [KSMETHODSETID \_ BdaDeviceConfiguration](./ksmethodsetid-bdadeviceconfiguration.md) 方法集的请求，以在当前筛选器关系图中为微型驱动程序配置筛选器实例。

在以下代码片段中，KSMETHODSETID BdaDeviceConfiguration 方法集的两个方法 \_ 均直接调度到 bda 支持库，并且 bda 微型驱动程序首先会截获剩余方法，然后再调度到 bda 支持库。

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

KSMETHOD \_ BDA \_ CREATE \_ 拓扑方法请求调用微型驱动程序的 CFilter：： CreateTopology 方法。 此方法将调用 BDA 支持库函数 [**BdaMethodCreateTopology**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdamethodcreatetopology) 以在筛选器 pin 之间创建拓扑。 此函数实际上在第3环中创建拓扑结构，该结构反映了筛选器的已知连接的其他属性集。 \_ \_ \_ 如果在连接特定的 pin 类型时微型驱动程序必须向硬件发送特殊说明，则 bda 微型驱动程序应截获 KSMETHOD BDA CREATE 拓扑方法请求，如前面的代码片段中所示; 例如，如果 BDA 设备执行硬件 demultiplexing 并从单个输入插针创建任意数量的输出插针。

 

