---
title: 更改 BDA 筛选器属性
description: 更改 BDA 筛选器属性
ms.assetid: 1833864a-5759-437c-ba60-0b38602d9e41
keywords:
- 属性设置 WDK BDA，筛选器属性更改
- 筛选器属性更改 WDK BDA
- 方法设置 WDK BDA，筛选器属性更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aafcd613c246846eb545362018b125a6c0e22caa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844738"
---
# <a name="changing-bda-filter-properties"></a>更改 BDA 筛选器属性





由于查看媒体广播的应用程序的多个实例可以同时在系统上运行，因此您应该编写一个 BDA 微型驱动程序来容纳多个筛选器实例。 每个筛选器实例可以包含不同的信息。 例如，一个调谐器筛选器实例可以包含优化到通道5的请求，而另一个实例则可以包含请求以优化到通道8。 当控件从一个实例转换为另一个实例时，BDA 微型驱动程序必须指示底层优化设备更改资源的配置方式。 BDA 微型驱动程序处理[KSMETHODSETID\_BdaChangeSync](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-bdachangesync)方法集的请求，该方法将设置为在一个微型驱动程序的筛选器实例上协调属性请求列表。

KSMETHODSETID\_BdaChangeSync 方法集的主要目的是提供一个触发器点，其中筛选器的基础微型驱动程序可以从微型驱动程序的设备对象获取和释放资源。 微型驱动程序必须协调这些触发器点，使筛选器与停止状态之间的转换。 例如，如果筛选器处于停止状态，则微型驱动程序应将新资源分配给筛选器，但只要网络提供程序指定提交 BDA 拓扑更改，就不会获取这些资源。 当筛选器随后转换为停止状态时，微型驱动程序应尝试从基础设备获取这些资源。

另一方面，如果筛选器已处于活动状态，则每当网络提供程序指定提交 BDA 拓扑更改时，微型驱动程序应尝试从基础设备获取新资源。 在任何给定时间，只有一个筛选器实例可以处于活动状态（处于运行状态并保存相同的资源）。 当某个筛选器转换为 "已停止" 状态时，它应释放其所有资源（包括为其任何 pin 分配的资源），以便资源可用于转换为 "正在运行" 状态的另一个筛选器图。

通常，BDA 微型驱动程序的筛选器对象会截获并提供 KSMETHODSETID\_BdaChangeSync 方法集的方法的方法。 例如，微型驱动程序提供用于启动、检查和提交筛选器更改以及获取筛选器更改状态的方法。 此外，以下微型驱动程序提供的方法应调用相应的 BDA 支持库函数，以便同步微型驱动程序之前已注册到 BDA 支持库的结构中的更改：

-   启动-更改方法调用[**BdaStartChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdastartchanges)函数。

-   检查更改方法调用[**BdaCheckChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacheckchanges)函数。

-   Commit-changes 方法会调用[**BdaCommitChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacommitchanges)函数。

-   获取更改状态的方法将调用[**BdaGetChangeState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdagetchangestate)函数。

下面的代码段演示如何使用内部方法来截获 KSMETHODSETID\_BdaChangeSync 方法集的方法请求：

```cpp
//
//  BDA Change Sync Method Set
//
//  Defines the dispatch routines for the filter level
//  Change Sync methods
//
DEFINE_KSMETHOD_TABLE(BdaChangeSyncMethods)
{
    DEFINE_KSMETHOD_ITEM_BDA_START_CHANGES(
        CFilter::StartChanges,
        NULL
        ),
    DEFINE_KSMETHOD_ITEM_BDA_CHECK_CHANGES(
        CFilter::CheckChanges,
        NULL
        ),
    DEFINE_KSMETHOD_ITEM_BDA_COMMIT_CHANGES(
        CFilter::CommitChanges,
        NULL
        ),
    DEFINE_KSMETHOD_ITEM_BDA_GET_CHANGE_STATE(
        CFilter::GetChangeState,
        NULL
        )
};
```

下面的代码段演示了在微型驱动程序调用**BdaStartChanges**支持函数以启动新 BDA 拓扑更改的设置之后，BDA 微型驱动程序中的内部启动-更改方法将重置挂起的资源更改：

```cpp
//
// StartChanges ()
//
//    Puts the filter into change state.  All changes to BDA topology
//    and properties changed after this will be in effect only after
//    CommitChanges.
//
NTSTATUS
CFilter::
StartChanges(
    IN PIRP         pIrp,
    IN PKSMETHOD    pKSMethod,
    OPTIONAL PVOID  pvIgnored
    )
{
    NTSTATUS        Status = STATUS_SUCCESS;
    CFilter *       pFilter;

    ASSERT( pIrp);
    ASSERT( pKSMethod);

    // Obtain a "this" pointer for the method.
    //
    // Because this function is called directly from the property 
    // dispatch table, must get pointer to the underlying object.
    //
    pFilter = FilterFromIRP( pIrp);
    ASSERT( pFilter);
    if (!pFilter)
    {
        Status = STATUS_INVALID_PARAMETER;
        goto errExit;
    }

    //  Reset any pending BDA topology changes.
    //
    Status = BdaStartChanges( pIrp);
    if (!NT_SUCCESS( Status))
    {
        goto errExit;
    }

    //  Reset any pending resource changes.
    //
    pFilter->m_NewTunerResource = pFilter->m_CurTunerResource;
    pFilter->m_BdaChangeState = BDA_CHANGES_COMPLETE;

errExit:
    return Status;
}
```

 

 




