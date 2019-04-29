---
title: 了解 Tracefmt
description: 了解 Tracefmt
ms.assetid: 614be46f-8c44-43da-b4ec-7fd7195e2c08
keywords:
- Tracefmt WDK，有关 Tracefmt
- TMF 文件 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d3c792dd3817124762658b1fca8c9c05c216c2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351783"
---
# <a name="understanding-tracefmt"></a>了解 Tracefmt


## <span id="ddk_understanding_tracefmt_tools"></span><span id="DDK_UNDERSTANDING_TRACEFMT_TOOLS"></span>


[跟踪提供程序](trace-provider.md)记录跟踪消息中以提高效率的二进制格式。 若要在可读的形式显示跟踪消息，Tracefmt 适用的格式设置的说明为每个消息，然后显示的消息或将它们保存在文本文件中。

> [!TIP]
> [TraceView](traceview.md)提供作为带有更易于使用 GUI Tracefmt 的相同功能。

跟踪提供程序使用 WPP 软件跟踪，然后将编译到 PDB 符号文件的私有或完整版本的跟踪提供程序的源代码中包含的跟踪消息的格式设置说明。 WPP 预处理器从私有符号中提取的格式设置的说明进行操作，并将它们放入[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)提供程序。

若要格式化跟踪消息，Tracefmt 需要 TMF 文件。 可以向 Tracefmt 或直接 Tracefmt TMF 文件创建为你提供 TMF 文件。 使用任何以下方法以提供所需的输入。

**使用 Default.tmf。** 由于大多数应用程序和驱动程序使用标准的消息格式，可使用 Default.tmf，WDK 中包含的文件中的信息格式设置它们的消息。

**提供一个 TMF 文件。** 可以通过提供其路径和文件名的名称来指定特定的 TMF 文件。

**提供 TMF 文件的目录的路径。** 可以使用 Tracefmt[消息 GUID](message-guid.md)的跟踪消息来确定包含 TMF 文件的目录中的消息的格式说明的 TMF 文件。 TMF 文件名称包含扩展名为.tmf 消息 GUID。

**直接 Tracefmt 创建 TMF 文件。** Tracefmt 可以使用跟踪提供程序的图像文件 （.exe、.dll 或.sys） 用于寻找跟踪提供程序专用的 PDB 符号文件的目录中或通过使用内部符号服务器。 然后从 PDB 文件中的数据创建 TMF 文件，并使用 TMF 文件来设置格式的跟踪消息。 当创建 TMF 文件时， [Tracepdb](tracepdb.md)创建[MOF](trace-managed-object-format--mof--file.md) (.mof) 文件，其中包含控件的 GUID 和 PDB 文件中表示的跟踪级别的每个跟踪提供程序。 MOF 文件的名称是跟踪提供程序的模块名称。

在格式设置的跟踪消息，Tracefmt 可以在命令行中显示跟踪消息，并且它可以创建以下文件：

- *输出文件*的格式化的跟踪消息。 消息出现在它们生成的跟踪提供程序的顺序。 每条消息被带有跟踪前缀。 有关信息，请参阅[跟踪消息前缀](trace-message-prefix.md)。

- 一个*条摘要消息文件*跟踪会话，在此期间生成的跟踪消息有关的信息。

有关事件跟踪的详细信息，请参阅 Microsoft Windows SDK 文档。 在驱动程序中使用事件跟踪的信息，请参阅[WPP 软件跟踪](wpp-software-tracing.md)。
