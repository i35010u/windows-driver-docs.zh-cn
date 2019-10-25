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
ms.openlocfilehash: 50f57c7916ccc552c658772faf54374420a1bb37
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844710"
---
# <a name="configuring-a-bda-filter"></a>配置 BDA 筛选器





BDA 微型驱动程序进程方法请求[KSMETHODSETID\_BdaDeviceConfiguration](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-bdadeviceconfiguration)方法集，以在当前筛选器关系图中为微型驱动程序配置筛选器实例。

在以下代码片段中，KSMETHODSETID\_BdaDeviceConfiguration 方法集的两个方法均直接调度到 BDA 支持库，并且在调度到 BDA 之前，将首先由 BDA 微型驱动程序截获剩余方法。支持库。

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

KSMETHOD\_BDA\_CREATE\_拓扑方法请求调用微型驱动程序的 CFilter：： CreateTopology 方法。 此方法将调用 BDA 支持库函数[**BdaMethodCreateTopology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdamethodcreatetopology)以在筛选器 pin 之间创建拓扑。 此函数实际上在第3环中创建拓扑结构，该结构反映了筛选器的已知连接的其他属性集。 如前面的代码片段中所示，BDA 微型驱动程序应截获 KSMETHOD\_BDA\_创建\_拓扑方法请求，前提是在连接特定的 pin 类型时微型驱动程序必须向硬件发送特殊指令--对于例如，如果 BDA 设备执行硬件 demultiplexing，并从单个输入插针创建任意数量的输出插针扇形展开。

 

 




