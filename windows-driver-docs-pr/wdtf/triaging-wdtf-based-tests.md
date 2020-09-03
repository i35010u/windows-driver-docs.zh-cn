---
title: 会审基于 WDTF 的测试
description: 为了帮助你更好地理解基于 WDTF 的测试中发生的情况，你可以使用内置的 WDTF 对象日志记录和 WPP 软件跟踪支持。
ms.assetid: C2F7AA74-7A74-4EA4-AD2D-8143252380C8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d3b6cb9f3b02965357b9225cdccdba778ef4e1
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403540"
---
# <a name="triaging-wdtf-based-tests"></a>会审基于 WDTF 的测试


为了帮助你更好地理解基于 WDTF 的测试中发生的情况，你可以使用内置的 [WDTF 对象日志记录](logging-and-tracing.md)和 [WPP 软件跟踪](../devtest/wpp-software-tracing.md)支持。

WDTF 对象日志记录导致 WDTF 对象 automatcially 将日志消息写入公用日志文件，这可以简化测试创作，并可帮助诊断测试问题。 设备基础测试以及在 WDK 中随附的其他测试都是基于 WDTF 的测试的示例。 有关这些测试的信息，请参阅 [如何选择和配置设备基础测试](/windows-hardware/drivers)。

WDTF 为 [WPP 软件跟踪](../devtest/wpp-software-tracing.md)提供支持。 所有 WDTF 对象都将在运行时生成跟踪信息。 可以使用 WDK 工具（包括 [TraceView](../devtest/using-traceview.md)）读取跟踪信息。

## <a name="in-this-section"></a>本节内容


-   [WDTF 对象日志记录](logging-and-tracing.md)
-   [启用和查看 WDTF 跟踪](viewing-wdtf-traces.md)
-   [对运行基于 WDTF 的测试时出现的问题进行诊断](diagnosing-problems-running-wdtf-based-tests.md)

 

