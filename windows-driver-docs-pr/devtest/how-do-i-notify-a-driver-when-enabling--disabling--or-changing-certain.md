---
title: 启用、禁用或更改某些标志时，如何实现通知驱动程序
description: 启用、禁用或更改某些标志时，如何实现通知驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddf03ef6f9cfd7ff4ba4fbd8282a49174359f7fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839127"
---
# <a name="how-do-i-notify-a-driver-when-enabling-disabling-or-changing-certain-flags"></a>启用、禁用或更改特定的标志时如何通知驱动程序？


当启用、禁用或更改跟踪标志时，某些驱动程序需要执行一些额外的工作。 若要在发生此类更改时通知驱动程序，请使用以下命令：

```
#define WPP_PRIVATE_ENABLE_CALLBACK 
```

必须先定义此符号常量，然后才能包含 TMH 文件。 需要编写的函数签名如下所示：

```
typedef
VOID
(*PFN_WPP_PRIVATE_ENABLE_CALLBACK)(
__in LPCGUID Guid,
__in __int64 Logger,
__in BOOLEAN Enable,
__in ULONG Flags,
__in UCHAR Level);
```

下面的示例演示如何在启用特定标志时通知驱动程序：

```
#define WPP_PRIVATE_ENABLE_CALLBACK MyOwnCallback
#include "tracedrv.tmh" // this is the file that will be auto-generated 
VOID MyOwnCallback (
                 __in LPCGUID Guid,
                 __in __int64 Logger,
                 __in BOOLEAN Enable,
                 __in ULONG Flags,
                 __in UCHAR Level) 
{
//                
//                  This callback function will be called with the current values of : GUID, Logger, Enable, Flags, and Level
//                 

                  if (Enable) {
                        .
                        .
                   }
} 
```









