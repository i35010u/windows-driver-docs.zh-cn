---
title: 用于启动 SIM 工具包的保留 URI
description: 用于启动 SIM 工具包的保留 URI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f1575b3587f9e9a72068ef9847023754fcd8cc7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837913"
---
# <a name="reserved-uri-to-launch-sim-toolkit"></a>用于启动 SIM 工具包的保留 URI


Windows 支持保留 URI 方案，使合作伙伴能够在 "开始" 屏幕上放置一个 UWP 应用程序，然后启动该应用程序的 CPL，使其更易发现。 目前，用户只能通过导航到 " **设置**" " &gt; **网络 & 无线** &gt; **移动电话 &" sim** &gt; **高级选项** "屏幕并点击" **SIM 应用程序** "按钮来访问 sim 应用程序。 有关详细信息，请参阅 [SIM 工具包](sim-toolkit.md)。

已 `"ms-settings-uicctoolkit"` 为 SIM 工具箱启动器定义 URI 方案。 这样，用户就可以更轻松地访问移动运营商网络（如银行或计费安全应用）的功能。

## <a name="launching-a-uri"></a>启动 URI


UWP 应用可以使用对 [ (LaunchUriAsync](/uwp/api/Windows.System.Launcher#Windows_System_Launcher_LaunchUriAsync_Windows_Foundation_Uri_)的调用) 方法从 **Windows.System** 命名空间的 **启动** 程序对象调用，来加载 SIM 应用程序 CPL。

下面的示例演示合作伙伴如何从应用启动 SIM 应用程序 CPL。

``` syntax
Windows.System.Launcher.LaunchUriAsync("ms-settings-uicctoolkit:");
```

## <a name="related-topics"></a>相关主题


[SIM 工具包](sim-toolkit.md)

 

