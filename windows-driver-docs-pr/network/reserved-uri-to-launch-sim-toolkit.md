---
title: 用于启动 SIM 工具包的保留 URI
description: 用于启动 SIM 工具包的保留 URI
ms.assetid: d194b37e-427b-4fe2-a49a-050d06a7d3b9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 322e0e454812b9c1a0c3dc4fd53188b0447110ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352991"
---
# <a name="reserved-uri-to-launch-sim-toolkit"></a>用于启动 SIM 工具包的保留 URI


Windows 包括对保留的 URI 方案，然后，可以启动以使其更易于被发现的 SIM 应用程序 CPL 的开始屏幕上放置的 UWP 应用的合作伙伴的支持。 目前，用户只能获取到 SIM 应用程序通过导航到**设置** &gt; **网络和无线** &gt; **移动电话和 SIM** &gt; **高级选项**屏幕并点击**SIM 应用程序**按钮。 有关详细信息，请参阅[SIM 工具包](sim-toolkit.md)。

URI 方案中， `"ms-settings-uicctoolkit"`，已为 SIM 工具包启动器定义。 这将使用户更轻松地访问功能，如银行或计费安全应用程序的移动运营商网络上。

## <a name="launching-a-uri"></a>启动 URI


UWP 应用可通过使用调用负载 SIM 应用程序 CPL [Launcher.LaunchUriAsync(Uri)](https://msdn.microsoft.com/library/windows/apps/hh701480.aspx)方法从**启动器**的对象**Windows.System**命名空间。

下面的示例演示如何合作伙伴可以启动应用程序中的 SIM 应用程序 CPL。

``` syntax
Windows.System.Launcher.LaunchUriAsync("ms-settings-uicctoolkit:");
```

## <a name="related-topics"></a>相关主题


[SIM 工具包](sim-toolkit.md)

 

 






