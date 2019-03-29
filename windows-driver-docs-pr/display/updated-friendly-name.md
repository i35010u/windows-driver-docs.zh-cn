---
title: WDDM 1.2 的已更新友好名称
description: 本主题介绍图形 INF 的新友好名称。 这是所有 Windows 8 中框显示驱动程序 Inf 可本地化的字符串名称要求。
ms.assetid: 26AE24C4-3C0D-4712-B66A-0B93FAD8043C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71c829989273bec11a093693ab75ad8d70fc7ea8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575590"
---
# <a name="updated-friendly-name-for-wddm-12"></a>WDDM 1.2 的已更新友好名称


本主题介绍图形 INF 的新友好名称。 这是所有 Windows 8 中框显示驱动程序 Inf 可本地化的字符串名称要求。

所有 Windows 8 内置驱动程序必须都使用 E3 功能得分，而不考虑的友好名称。 友好名称将反映支持此处所述 INF 的驱动程序模型。

在 Windows 8 上测试，而且在 Windows 8 中，(Microsoft Corporation 的 WDDM v1.2) 框中包含的 Windows 显示器驱动程序模型 (WDDM) 1.2 驱动程序必须在名称后追加设备，在此示例中所示：

``` syntax
;
; Localizable Strings
;
IHV_DeviceName.XXX = "My Device Name (Microsoft Corporation - WDDM v1.2)"
```

**请注意**  以轻松地突出显示要启用 Windows 8 特有的可选功能，针对 Windows 8 进行了优化，仅，用于测试驱动程序，我们建议以下输入，以便用户能够轻松地确定它不是标准 Windows 8 驱动程序。 （这应该还使 bug 更轻松地会审）。

 

例如：WDDM 1.2 特定工作

``` syntax
IHV_DeviceName.XXX = "My Device Name (Engineering Sample - WDDM v1.2)"
```

在 Windows 8 上测试，而且在 Windows 8 中，(Microsoft Corporation 的 WDDM 1.1 版) 框中包含的 WDDM 1.1 驱动程序必须在名称后追加设备，在此示例中所示：

``` syntax
;
; Localizable Strings
;
IHV_DeviceName.XXX = "My Device Name (Microsoft Corporation - WDDM v1.1)"
```

在 Windows 8 上测试，而且在 Windows 8 中，(Microsoft Corporation 的 WDDM v1.0) 框中包含的 WDDM 1.0 驱动程序必须在名称后追加设备，在此示例中所示：

``` syntax
;
; Localizable Strings
;
IHV_DeviceName.XXX = "My Device Name (Microsoft Corporation - WDDM v1.0)"
```

 

 





