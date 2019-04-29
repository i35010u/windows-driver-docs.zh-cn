---
title: 日志记录清单概述
description: 日志记录清单概述
ms.assetid: abf550c5-6b70-4043-b2e9-d3dc5096cc4e
keywords:
- 日志查看器，清单
- 日志查看器，清单，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eea59260a5928503ff0e670758c24d5983bbf9b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366458"
---
# <a name="overview-of-the-logging-manifest"></a>日志记录清单概述


## <span id="ddk_overview_of_the_logging_manifest_dtoolq"></span><span id="DDK_OVERVIEW_OF_THE_LOGGING_MANIFEST_DTOOLQ"></span>


日志记录清单是定义的函数和拦截和记录的 COM 接口的"标头"文件组。 这些不是，则返回 trueC++标头文件，它们是显式声明所需的记录器的信息的略有不同格式。

例如，清单格式的功能包括以下功能：

-   OUT 参数的名称。 这些是应记录在自己的方式执行函数以及被淘汰的参数。

-   定义的标志掩码。 此功能允许日志查看器来分解成更易于阅读其构成位标签的 DWORD 标记。

-   失败的情况下的定义。 此功能允许日志查看器来添加阴影的函数返回了失败状态代码或另一个错误代码的行。 此外，如果该函数将设置线程的"LastError"值，日志查看器可以存储消失的错误代码和扩展到其相应的用户可读的错误消息。

-   可以使用别名的日志差异的参数的名称。 此功能提供日志查看器将常量字符串分配给指针和句柄等变化执行执行时的数据导出到文件的值的选项。 然后可以使用差异比较工具来比较两个执行日志的差异。 如果指针和句柄值不是使用别名，它们将在两个文件进行比较时产生不相关的差异。

 

 





