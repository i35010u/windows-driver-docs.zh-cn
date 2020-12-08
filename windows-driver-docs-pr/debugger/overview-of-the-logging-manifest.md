---
title: 日志记录清单概述
description: 日志记录清单概述
keywords:
- LogViewer，清单
- LogViewer，清单，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: db12a895256dcac1494d3195ba9abe12d0461e0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834713"
---
# <a name="overview-of-the-logging-manifest"></a>日志记录清单概述


## <span id="ddk_overview_of_the_logging_manifest_dtoolq"></span><span id="DDK_OVERVIEW_OF_THE_LOGGING_MANIFEST_DTOOLQ"></span>


日志记录清单是一组 "标头" 文件，用于定义截获和记录的函数和 COM 接口。 它们不是真正的 c + + 头文件，它们采用略有不同的格式，可显式声明记录器所需的信息。

例如，清单格式有助于以下功能：

-   指定 OUT 参数。 这两个参数都应同时记录在函数中，同时也会在外进行。

-   标记掩码的定义。 此功能允许 LogViewer 将 DWORD 标志拆分为其构成位标签，以便于阅读。

-   故障事例的定义。 此功能允许 LogViewer 为已返回失败状态代码的函数行或其他错误代码设置底纹。 此外，如果该函数为线程设置了 "LastError" 值，则 LogViewer 可以存储错误代码，并将其扩展到其对应的可读错误消息。

-   指定可以为日志差分指定别名的参数。 此功能为 LogViewer 提供了在将数据导出到文件时，为从执行更改为执行（如指针和句柄）的值的选项。 然后，可以使用差异比较工具比较两个执行日志的差异。 如果指针和句柄值没有化名，它们会在比较两个文件时产生不相关的差异。

 

 





