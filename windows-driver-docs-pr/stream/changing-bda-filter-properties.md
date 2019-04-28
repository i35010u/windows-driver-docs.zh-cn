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
ms.openlocfilehash: e5f2d456e8e19154c4d5d1c3012defd46343c9c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351851"
---
# <a name="changing-bda-filter-properties"></a>更改 BDA 筛选器属性





因为视图媒体广播可以同时运行的系统的应用程序的多个实例，您应编写 BDA 微型驱动程序以适应一个筛选器的多个实例。 每个筛选器实例可以包含不同的信息。 例如，调谐器筛选器的一个实例可以包含调到频道 5，而另一个实例可以包含调到第 8 频道的请求的请求。 控件从一个实例转换到另一个，如 BDA 微型驱动程序必须指示基础优化设备，若要更改的资源配置的方式。 BDA 微型驱动程序处理的方法请求[KSMETHODSETID\_BdaChangeSync](https://msdn.microsoft.com/library/windows/hardware/ff563403)微型驱动程序的筛选器实例上一个请求方法设置来协调一组属性。

KSMETHODSETID 的主要用途\_BdaChangeSync 方法集是提供触发点筛选器基础微型驱动程序可以获取和释放资源从微型驱动程序的设备对象。 微型驱动程序必须协调这些触发点与筛选器转换到和从已停止状态。 例如，如果筛选器是处于停止状态，微型驱动程序应将新的资源分配给筛选器，但不是获取这些资源，只要提交 BDA 拓扑更改到指定的网络提供程序。 当筛选器随后转换从其已停止状态时，微型驱动程序应尝试获取这些资源从基础设备。

另一方面，如果筛选器已处于活动状态，微型驱动程序应尝试获取基础设备中的新资源，只要提交 BDA 拓扑更改到指定的网络提供程序。 只有一个筛选器的实例可以在运行状态和相同的资源--保存在任何给定时间中处于活动状态。 当筛选器转换为已停止状态时，因此应当将释放所有资源，包括所分配的任何其插针，这些资源，使资源可供将转换为正在运行状态的另一个筛选器关系图。

通常情况下，BDA 微型驱动程序的筛选器对象截获，并提供了方法的方法的 KSMETHODSETID\_BdaChangeSync 方法集。 例如，微型驱动程序提供了用于启动、 检查和提交筛选器更改以及获取筛选器的更改状态的方法。 此外，微型驱动程序提供的以下方法应调用相应的 BDA 支持同步微型驱动程序以前已注册 BDA 支持库的结构上的更改的库函数：

-   开始更改方法调用[ **BdaStartChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff556507)函数。

-   检查更改方法调用[ **BdaCheckChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff556433)函数。

-   提交更改方法调用[ **BdaCommitChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff556435)函数。

-   获取已更改状态方法调用[ **BdaGetChangeState** ](https://msdn.microsoft.com/library/windows/hardware/ff556458)函数。

下面的代码段演示如何以截获方法请求的 KSMETHODSETID\_BdaChangeSync 方法使用的内部方法设置：

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

以下代码片段演示如何 BDA 微型驱动程序中的内部开始更改方法重置挂起资源更改后的微型驱动程序调用**BdaStartChanges**支持函数启动新 BDA 拓扑的设置更改：

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

 

 




