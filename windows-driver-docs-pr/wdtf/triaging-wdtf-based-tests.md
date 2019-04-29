---
title: 会审基于 WDTF 的测试
description: 为了帮助您更好地了解这怎么回事 WDTF 基于测试中，可以为 WDTF 对象日志记录和 WPP 软件跟踪使用的内置支持。
ms.assetid: C2F7AA74-7A74-4EA4-AD2D-8143252380C8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c026384159c004d68b28952d973f61f039cd1bb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365517"
---
# <a name="triaging-wdtf-based-tests"></a>会审基于 WDTF 的测试


为了帮助你更好地理解基于 WDTF 的测试中发生的情况，你可以使用内置的 [WDTF 对象日志记录](logging-and-tracing.md)和 [WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556204)支持。

WDTF 对象日志记录会导致到 automatcially WDTF 对象编写日志消息到常见的日志文件，可以简化测试创作，可帮助你诊断测试问题。 设备基础测试和其他在 WDK 中提供的测试是基于 WDTF 的测试的示例。 有关这些测试的信息，请参阅[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)。

WDTF 提供支持[WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556204)。 在运行时，所有 WDTF 对象都生成的跟踪信息。 可以通过使用 WDK 工具，包括读取跟踪信息[TraceView](https://msdn.microsoft.com/library/windows/hardware/ff556063)。

## <a name="in-this-section"></a>本节内容


-   [WDTF 对象日志记录](logging-and-tracing.md)
-   [启用和查看 WDTF 跟踪](viewing-wdtf-traces.md)
-   [诊断运行 WDTF 基于测试问题](diagnosing-problems-running-wdtf-based-tests.md)

 

 




