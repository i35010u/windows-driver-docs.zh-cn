---
title: 如何通知时启用、 禁用或更改某些标志的驱动程序
description: 如何通知时启用、 禁用或更改某些标志的驱动程序
ms.assetid: 1bdf8047-8d3f-4cdf-883b-3544dea06705
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa2f2156dcf1d1917d44fb7abb33af31c08533a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547369"
---
# <a name="how-do-i-notify-a-driver-when-enabling-disabling-or-changing-certain-flags"></a>如何通知时启用、 禁用或更改某些标志的驱动程序？


某些驱动程序需要执行一些附加工作时启用、 禁用或更改跟踪标志。 若要通知一个驱动程序，发生此类更改时，请使用以下命令：

```
#define WPP_PRIVATE_ENABLE_CALLBACK 
```

包括 TMH 文件之前，必须定义此符号常量。 您需要编写的函数签名如下所示：

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

下面是方式的启用的某些标志时通知驱动程序的示例：

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









