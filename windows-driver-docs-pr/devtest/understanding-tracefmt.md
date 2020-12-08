---
title: 了解 Tracefmt
description: 了解 Tracefmt
keywords:
- Tracefmt WDK，关于 Tracefmt
- TMF 文件 WDK，Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 720932edcdaffb04eb95ec8c67871ff29e2fc2e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830103"
---
# <a name="understanding-tracefmt"></a>了解 Tracefmt


## <span id="ddk_understanding_tracefmt_tools"></span><span id="DDK_UNDERSTANDING_TRACEFMT_TOOLS"></span>


[跟踪提供程序](trace-provider.md) 以二进制形式记录跟踪消息，以便提高效率。 若要以可读形式显示跟踪消息，Tracefmt 将对每条消息应用格式说明，然后显示消息或将其保存在文本文件中。

> [!TIP]
> [TraceView](traceview.md) 提供与 Tracefmt 相同的有趣和易于使用的 GUI。

跟踪消息的格式设置说明包含在使用 WPP 软件跟踪的跟踪提供程序的源代码中，然后编译到跟踪提供程序的 PDB 符号文件的私有版本或完整版本。 WPP 预处理器从私有符号中提取格式说明，并将其放置在提供程序 [ ( 的跟踪消息格式) 文件](trace-message-format-file.md) 中。

若要设置跟踪消息的格式，Tracefmt 需要一个 TMF 文件。 你可以向 Tracefmt 或定向 Tracefmt 提供 TMF 文件，为你创建一个 TMF 文件。 使用以下任一方法来提供所需的输入。

**使用 tmf。** 由于大多数应用程序和驱动程序使用标准消息格式，因此可以使用 tmf 中包含的文件的信息来格式化其消息。

**提供 TMF 文件。** 可以通过提供特定 TMF 文件的路径和文件名来指定该文件。

**提供 TMF 文件的目录的路径。** Tracefmt 可以使用跟踪消息的 [消息 GUID](message-guid.md) 来识别包含 TMF 文件目录中消息的格式说明的 TMF 文件。 TMF 文件的名称包含 TMF 文件扩展名的消息 GUID。

**直接 Tracefmt 创建 TMF 文件。** Tracefmt 可以使用、.dll 或 .sys) 的图像 ( 文件为跟踪提供程序查找目录中跟踪提供程序的私有 PDB 符号文件或使用内部符号服务器。 然后，它从 PDB 文件中的数据创建 TMF 文件，并使用 TMF 文件来格式化跟踪消息。 当创建 TMF 文件时， [Tracepdb](tracepdb.md) 会创建一个 [mof](trace-managed-object-format--mof--file.md) ( mof) 文件，其中包含 PDB 文件中表示的每个跟踪提供程序的控件 GUID 和跟踪级别。 MOF 文件的名称为跟踪提供程序的模块名称。

格式化跟踪消息后，Tracefmt 可以在命令行中显示跟踪消息，并可以创建以下文件：

- 格式化跟踪消息的 *输出文件* 。 消息按照跟踪提供程序生成的顺序显示。 每条消息前面都有一个跟踪前缀。 有关信息，请参阅 [跟踪消息前缀](trace-message-prefix.md)。

- *摘要消息文件*，其中生成跟踪消息期间有关跟踪会话的信息。

有关事件跟踪的详细信息，请参阅 Microsoft Windows SDK 文档。 有关使用驱动程序中的事件跟踪的信息，请参阅 [WPP 软件跟踪](wpp-software-tracing.md)。
