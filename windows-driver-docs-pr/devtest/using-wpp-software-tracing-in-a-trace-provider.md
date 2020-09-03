---
title: 在跟踪提供程序中使用 WPP 软件跟踪
description: 在跟踪提供程序中使用 WPP 软件跟踪
ms.assetid: e215a99b-5082-4e81-84b6-184a2fd4e270
keywords:
- Windows 软件跟踪预处理器 WDK，关于 WPP
- WPP 软件跟踪 WDK，关于 WPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca80b4ffbfa96663826442e52c8ad81fe806ee5e
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385077"
---
# <a name="using-wpp-software-tracing-in-a-trace-provider"></a>在跟踪提供程序中使用 WPP 软件跟踪


## <span id="ddk_using_wpp_software_tracing_in_a_driver_tools"></span><span id="DDK_USING_WPP_SOFTWARE_TRACING_IN_A_DRIVER_TOOLS"></span>


若要在 [跟踪提供程序](trace-provider.md)中使用 WPP 软件跟踪的默认形式，例如内核模式驱动程序或用户模式应用程序，请执行以下操作：

-   定义唯一标识 [跟踪提供程序](trace-provider.md)的控件 GUID。 提供程序在其 [WPP \_ 控制 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏的定义和 [Tracelog](tracelog.md)使用的相关控件文件中指定此 GUID。

-   如 [将 Wpp 宏添加到跟踪提供程序](adding-wpp-macros-to-a-trace-provider.md) 和 [Wpp 软件跟踪引用](/previous-versions/windows/hardware/previsioning-framework/ff556205(v=vs.85))中所述，将所需的与 wpp 相关的 C 预处理器指令和 WPP 宏调用添加到提供程序的源文件中。

-   构建驱动程序，如 [WPP 预处理器](wpp-preprocessor.md)中所述。

-   使用其他工具进行软件跟踪，如 [TraceView](traceview.md)、 [Tracelog](tracelog.md)、 [Tracefmt](tracefmt.md)和 [Tracepdb](tracepdb.md) ，以配置、启动和停止跟踪会话并显示和筛选跟踪消息。 这些工具包含在 Windows 驱动程序工具包 (WDK) 在 "工具" " \\ \\ 跟踪目录" 中。

 

