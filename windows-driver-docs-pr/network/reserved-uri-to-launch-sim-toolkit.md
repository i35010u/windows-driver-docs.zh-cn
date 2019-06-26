---
title: 用于启动 SIM 工具包的保留 URI
description: 用于启动 SIM 工具包的保留 URI
ms.assetid: d194b37e-427b-4fe2-a49a-050d06a7d3b9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d73bc5dc34995eec6854464553fab1d7e53f0edb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384711"
---
# <a name="reserved-uri-to-launch-sim-toolkit"></a>用于启动 SIM 工具包的保留 URI


Windows 包括对保留的 URI 方案，然后，可以启动以使其更易于被发现的 SIM 应用程序 CPL 的开始屏幕上放置的 UWP 应用的合作伙伴的支持。 目前，用户只能获取到 SIM 应用程序通过导航到**设置** &gt; **网络和无线** &gt; **移动电话和 SIM** &gt; **高级选项**屏幕并点击**SIM 应用程序**按钮。 有关详细信息，请参阅[SIM 工具包](sim-toolkit.md)。

URI 方案中， `"ms-settings-uicctoolkit"`，已为 SIM 工具包启动器定义。 这将使用户更轻松地访问功能，如银行或计费安全应用程序的移动运营商网络上。

## <a name="launching-a-uri"></a>启动 URI


UWP 应用可通过使用调用负载 SIM 应用程序 CPL [Launcher.LaunchUriAsync(Uri)](https://docs.microsoft.com/uwp/api/Windows.System.Launcher#Windows_System_Launcher_LaunchUriAsync_Windows_Foundation_Uri_)方法从**启动器**的对象**Windows.System**命名空间。

下面的示例演示如何合作伙伴可以启动应用程序中的 SIM 应用程序 CPL。

``` syntax
Windows.System.Launcher.LaunchUriAsync("ms-settings-uicctoolkit:");
```

## <a name="related-topics"></a>相关主题


[SIM 工具包](sim-toolkit.md)

 

 






