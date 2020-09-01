---
title: 处理通知标注
description: 处理通知标注
ms.assetid: d686989e-97f0-4095-b172-1c2ccf7a26e6
keywords:
- Windows 筛选平台标注驱动程序 WDK，通知标注
- 标注驱动程序 WDK Windows 筛选平台，通知标注
- notifyFn
- 通知标注 WDK Windows 筛选平台
- Windows 筛选平台标注驱动程序 WDK、筛选器添加和删除
- 标注驱动程序 WDK Windows 筛选平台，筛选添加和删除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce3855fa8d0585c274e848c997a16a29e29aade0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215184"
---
# <a name="processing-notify-callouts"></a>处理通知标注


筛选器引擎调用标注的 [*notifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0) callout 函数，以通知标注驱动程序与标注关联的事件。

### <a name="filter-addition"></a><a href="" id="filter-addition"></a> 筛选器加法

当指定筛选器操作的标注的筛选器添加到筛选器引擎时，筛选器引擎将调用标注的 [*notifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0) callout 函数，并 \_ \_ \_ \_ 在 *notifyType* 参数中传递 FWPS callout 通知添加筛选器。

标注驱动程序可以在指定筛选器操作的标注的筛选器已添加到筛选器引擎之后，使用筛选器引擎注册标注。 在这种情况下，筛选器引擎不调用标注的 [*notifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0) callout 函数来通知标注有关现有筛选器的信息。

筛选器引擎仅在指定筛选器操作的标注的新筛选器添加到筛选器引擎时，才调用标注的 *notifyFn* callout 函数来通知标注。 在这种情况下，可能不会为筛选器引擎中指定筛选器操作的标注的每个筛选器调用标注的 *notifyFn* 标注函数。

如果标注驱动程序在筛选器引擎开始后注册标注，而且标注必须收到有关筛选器引擎中指定标注的筛选器的每个筛选器的信息，则标注驱动程序必须调用适当的管理函数以枚举筛选器引擎中的所有筛选器。 标注驱动程序必须按所有筛选器的结果列表进行排序，才能查找指定筛选器操作标注的筛选器。 有关调用这些函数的详细信息，请参阅 [调用其他 Windows 筛选平台函数](calling-other-windows-filtering-platform-functions.md) 。

### <a name="filter-deletion"></a><a href="" id="filter-deletion"></a> 筛选器删除

如果从筛选器引擎中删除指定筛选器操作的标注的筛选器，则筛选器引擎将调用标注的[*notifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0) callout 函数并 \_ \_ \_ 在 notifyType 参数中传递 FWPS callout 通知删除筛选器，并在 \_ *filterKey*参数中传递**NULL** 。 *notifyType* 对于指定筛选器操作的标注的筛选器引擎中，筛选器引擎为每个已删除的筛选器调用标注的 *notifyFn* 标注函数。 这包括标注驱动程序将标注注册到筛选器引擎之前添加到筛选器引擎的任何筛选器。 因此，对于未接收筛选器添加通知的筛选器，标注可能会收到筛选器删除通知。

如果标注的 [*notifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0) callout 函数无法识别在 *notifyType* 参数中传递的通知类型，它应忽略通知并返回状态 " \_ 成功"。

标注驱动程序可以指定在将筛选器添加到筛选器引擎时要与筛选器关联的上下文。 此类上下文对于筛选器引擎是不透明的。 标注的 [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) callout 函数可以使用此上下文保存状态信息，以便在筛选器引擎下次调用时保存状态信息。 从筛选器引擎中删除筛选器后，标注驱动程序将执行任何所需的上下文清理。

例如：

```C++
// Context structure to be associated with the filters
typedef struct FILTER_CONTEXT_ {
  .
  .  // Driver-specific content
  .
} FILTER_CONTEXT, *PFILTER_CONTEXT;

// Memory pool tag for filter context structures
#define FILTER_CONTEXT_POOL_TAG 'fcpt'

// notifyFn callout function
NTSTATUS NTAPI
 NotifyFn(
    IN FWPS_CALLOUT_NOTIFY_TYPE  notifyType,
    IN const GUID  *filterKey,
    IN const FWPS_FILTER0  *filter
    )
{
  PFILTER_CONTEXT context;

 ASSERT(filter != NULL);

  // Switch on the type of notification
 switch(notifyType) {

    // A filter is being added to the filter engine
 case FWPS_CALLOUT_NOTIFY_ADD_FILTER:

      // Allocate the filter context structure
 context =
        (PFILTER_CONTEXT)ExAllocatePoolWithTag(
 NonPagedPool,
 sizeof(FILTER_CONTEXT),
          FILTER_CONTEXT_POOL_TAG
          );

      // Check the result of the memory allocation
 if (context == NULL) {

        // Return error
 return STATUS_INSUFFICIENT_RESOURCES;
      }

      // Initialize the filter context structure
      ...

      // Associate the filter context structure with the filter
 filter->context = (UINT64)context;

 break;

    // A filter is being removed from the filter engine
 case FWPS_CALLOUT_NOTIFY_DELETE_FILTER:

      // Get the filter context structure from the filter
 context = (PFILTER_CONTEXT)filter->context;

 // Check whether the filter has a context
 if (context) {

        // Cleanup the filter context structure
        ...

        // Free the memory for the filter context structure
 ExFreePoolWithTag(
 context,
          FILTER_CONTEXT_POOL_TAG
          );

      }
 break;

    // Unknown notification
 default:

      // Do nothing
 break;
  }

 return STATUS_SUCCESS;
}
```

 

