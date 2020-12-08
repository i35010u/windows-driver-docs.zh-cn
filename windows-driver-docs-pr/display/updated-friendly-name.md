---
title: WDDM 1.2 的已更新友好名称
description: 本主题介绍图形 INF 的已更新的友好名称。 对于所有 Windows 8 内置的显示驱动程序 Inf，这是一个可本地化的字符串名称要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50787ee5f1f8466ffa807485e6f00c9acfd177c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802549"
---
# <a name="updated-friendly-name-for-wddm-12"></a>WDDM 1.2 的已更新友好名称


本主题介绍图形 INF 的已更新的友好名称。 对于所有 Windows 8 内置的显示驱动程序 Inf，这是一个可本地化的字符串名称要求。

无论友好名称如何，所有 Windows 8 内置驱动程序都必须使用 E3 功能分数。 友好名称将反映此处所述 INF 支持的驱动程序模型。

对于 Windows 显示器驱动程序模型 (在 Windows 8 上测试并包含在 Windows 8 中的框中的) 1.2 驱动程序， (Microsoft Corporation-WDDM v2.0) 必须追加到设备名称上，如以下示例中所示：

``` syntax
;
; Localizable Strings
;
IHV_DeviceName.XXX = "My Device Name (Microsoft Corporation - WDDM v1.2)"
```

**注意**  
若要轻松突出显示仅用于测试的驱动程序，将启用针对 Windows 8 优化的特定于 Windows 8 的可选功能，我们建议使用以下输入，以便用户可以轻松确定它不是标准 Windows 8 驱动程序。  (这还应该使 bug 更易于) 的会审。

 

例如： WDDM 1.2 特定工作

``` syntax
IHV_DeviceName.XXX = "My Device Name (Engineering Sample - WDDM v1.2)"
```

对于在 Windows 8 上测试并包含在 Windows 8 中的框中的 WDDM 1.1 驱动程序， (Microsoft Corporation-WDDM v1.1) 必须追加到设备名称上，如以下示例中所示：

``` syntax
;
; Localizable Strings
;
IHV_DeviceName.XXX = "My Device Name (Microsoft Corporation - WDDM v1.1)"
```

对于在 Windows 8 上测试并包含在 Windows 8 中的框中的 WDDM 1.0 驱动程序， (Microsoft Corporation-WDDM v1.0) 必须追加到设备名称上，如以下示例中所示：

``` syntax
;
; Localizable Strings
;
IHV_DeviceName.XXX = "My Device Name (Microsoft Corporation - WDDM v1.0)"
```

 

 





