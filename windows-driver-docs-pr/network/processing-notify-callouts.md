---
title: 处理通知标注
description: 处理通知标注
ms.assetid: d686989e-97f0-4095-b172-1c2ccf7a26e6
keywords:
- Windows 筛选平台标注驱动程序 WDK，通知标注
- 标注驱动程序 WDK Windows 筛选平台，通知标注
- notifyFn
- 通知标注 WDK Windows 筛选平台
- Windows 筛选平台标注驱动程序 WDK，筛选器添加和删除操作
- 标注驱动程序 WDK Windows 筛选平台，筛选器添加和删除操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c8c1c6ef8155b032951d64458926aa991894737
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327631"
---
# <a name="processing-notify-callouts"></a>处理通知标注


筛选器引擎将调用一个标注[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)标注函数，以通知有关与标注相关联的事件的标注驱动程序。

### <a href="" id="filter-addition"></a> 筛选器添加

当指定的筛选器操作添加到筛选器引擎标注的筛选器，筛选器引擎调用的标注[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)标注函数，传递 FWPS\_标注\_通知\_添加\_筛选*notifyType*参数。

后指定筛选器的操作的标注的筛选器已添加到筛选器引擎，标注驱动程序可以使用筛选器引擎注册一个标注。 在此情况下，筛选器引擎不会调用的标注[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)标注函数，以通知有关的任何现有筛选器的标注。

筛选器引擎仅调用的标注*notifyFn*标注函数，以指定筛选器的操作的标注的新筛选器添加到筛选器引擎时通知标注。 在此情况下，一个标注的*notifyFn*标注函数可能不会调用中指定的筛选器操作的标注的筛选器引擎的每个筛选器。

如果标注驱动程序筛选器引擎启动和标注必须接收有关每个筛选器信息中指定的筛选器操作的标注的筛选器引擎后注册一个标注，标注驱动程序必须调用合适的管理若要枚举筛选器引擎中的所有筛选器的功能。 标注驱动程序必须对通过生成的所有筛选器以查找指定的筛选器操作的标注这些筛选器列表进行排序。 请参阅[调用其他 Windows 筛选平台函数](calling-other-windows-filtering-platform-functions.md)有关调用这些函数的详细信息。

### <a href="" id="filter-deletion"></a> 筛选器删除

当指定一个标注的筛选器引擎中删除筛选器的操作筛选器，筛选器引擎调用的标注[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)标注函数并传递 FWPS\_标注\_通知\_删除\_筛选*notifyType*参数和**NULL**中*filterKey*参数。 筛选器引擎将调用的标注*notifyFn*标注函数中指定的筛选器操作的标注的筛选器引擎的每个已删除筛选器。 这包括已添加到筛选器引擎标注驱动程序筛选器引擎注册标注之前的任何筛选器。 因此，一个标注可能会收到筛选器删除通知，如为其未收到筛选器的筛选器，可添加通知。

如果的标注[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)标注函数不能识别传入的通知类型*notifyType*参数，则它应忽略通知并返回状态\_成功。

标注驱动程序可以指定筛选器添加到筛选器引擎时要与筛选器相关联的上下文。 此类上下文是不透明的筛选器引擎。 标注[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)标注函数可以使用此上下文以保存筛选器引擎通过调用下一次的状态信息。 从筛选器引擎中删除筛选器，标注驱动程序将执行上下文的任何必要的清理。

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

 

 





