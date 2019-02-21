---
title: 示例 3 指定 TMF 文件
description: 示例 3 指定 TMF 文件
ms.assetid: 202304f0-7f8e-4ad1-b10c-185c33db1498
keywords:
- Tracefmt WDK，TMF 文件
- TMF 文件 WDK，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d83a2a1899393f503f6efddd514de426823471f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523323"
---
# <a name="example-3-specifying-a-tmf-file"></a>示例 3：指定 TMF 文件

此示例演示指定用来设置格式的跟踪消息的 TMF 文件的方法：

-   使用 **-tmf**参数。

    下面的命令使用 **-tmf**参数来指定 TMF 文件路径和文件名。 路径重写任何其他 TMF 路径规范。

    ```
    tracefmt mytrace.etl -tmf c:\tracing\37753236-c81f-505e-d40a-128d3bb2b5ff.tmf
    ```

    Tracefmt 使用指定的 TMF 文件来设置 mytrace.etl 文件中的跟踪消息的格式。

-   使用 **-p**参数。

    下面的命令使用 **-p**参数来指定 TMF 文件所在的目录。 Tracefmt 匹配控件的跟踪提供程序具有 TMF 文件名称，以查找正确的 TMF 文件的 GUID。 这使用户无需复制或键入繁琐的 GUID 文件名称。

    ```
    tracefmt mytrace.etl -p c:\tracing
    ```

    Tracefmt 使用指定的 TMF 文件来设置 mytrace.etl 文件中的跟踪消息的格式。

-   使用 %跟踪\_格式\_搜索\_路径 %。

    本系列中的第一个命令设置的值 %跟踪\_格式\_搜索\_PATH %环境变量为目录位置，在这种情况下，c:\\跟踪。

    在其后，Tracefmt 命令 **-tmf**并 **-p**省略了参数。

    ```
    set TRACE_FORMAT_SEARCH_PATH=c:\tracing
    tracefmt mytrace.etl
    ```

    Tracefmt 尽管 Tracefmt 命令中指定一个路径既不是目录，搜索在 c:\\TMF 文件，然后使用内容格式化跟踪消息 mytrace.etl 文件中的跟踪目录。

如果指定的任何一种方法 TMF 文件不包括格式设置的跟踪消息，说明[TraceView](traceview.md)将消息写入到输出文件并显示"未找到格式信息"错误消息。 例如：

```text
Unknown( 10): GUID=37753236-c81f-505e-d40a-128d3bb2b5ff (No Format Information found).
Unknown( 11): GUID=37753236-c81f-505e-d40a-128d3bb2b5ff (No Format Information found).
Unknown( 11): GUID=37753236-c81f-505e-d40a-128d3bb2b5ff (No Format Information found).
...
```
