---
title: 示例3指定 TMF 文件
description: 示例3指定 TMF 文件
keywords:
- Tracefmt WDK，TMF 文件
- TMF 文件 WDK，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d39a01966a08b6a6a69b2576657e90c48fa9788
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839143"
---
# <a name="example-3-specifying-a-tmf-file"></a>示例 3：指定 TMF 文件

此示例演示了指定 TMF 文件的方法，这些方法用于设置跟踪消息的格式：

-   使用 **-tmf** 参数。

    以下命令使用 **-tmf** 参数来指定 tmf 文件的路径和文件名。 该路径将覆盖任何其他 TMF 路径规范。

    ```
    tracefmt mytrace.etl -tmf c:\tracing\37753236-c81f-505e-d40a-128d3bb2b5ff.tmf
    ```

    Tracefmt 使用指定的 TMF 文件对 mytrace 文件中的跟踪消息进行格式设置。

-   使用 **-p** 参数。

    以下命令使用 **-p** 参数来指定 TMF 文件所在的目录。 Tracefmt 将跟踪提供程序的控件 GUID 与 TMF 文件名匹配，以便查找正确的 TMF 文件。 这样，用户不必复制或键入繁琐的 GUID 文件名。

    ```
    tracefmt mytrace.etl -p c:\tracing
    ```

    Tracefmt 使用指定的 TMF 文件对 mytrace 文件中的跟踪消息进行格式设置。

-   使用% 跟踪 \_ 格式 \_ 搜索 \_ 路径%。

    此系列中的第一个命令将% TRACE \_ FORMAT \_ SEARCH \_ PATH% 环境变量的值设置为目录位置，在本例中为 c： TRACE \\ 。

    在其后跟在 Tracefmt 命令中，将省略 **-tmf** 和 **-p** 参数。

    ```
    set TRACE_FORMAT_SEARCH_PATH=c:\tracing
    tracefmt mytrace.etl
    ```

    尽管路径和目录均未在 Tracefmt 命令中指定，但 Tracefmt 会搜索 TMF 文件的 c： \\ trace 目录，然后使用该内容设置 mytrace 文件中跟踪消息的格式。

如果这些方法中的任何一种指定的 TMF 文件不包括跟踪消息的格式说明，则 [TraceView](traceview.md) 会将消息写入输出文件，其中包含 "找不到格式信息" 错误消息。 例如：

```text
Unknown( 10): GUID=37753236-c81f-505e-d40a-128d3bb2b5ff (No Format Information found).
Unknown( 11): GUID=37753236-c81f-505e-d40a-128d3bb2b5ff (No Format Information found).
Unknown( 11): GUID=37753236-c81f-505e-d40a-128d3bb2b5ff (No Format Information found).
...
```
