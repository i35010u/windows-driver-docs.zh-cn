---
title: TraceView -parsepdb
description: 使用 TraceView-parsepdb 命令从 PDB 符号文件中的数据创建跟踪消息格式的文件。
ms.assetid: d193aa3c-17ee-4fcf-a4ee-afb50c78ec54
keywords:
- TraceView-parsepdb 驱动程序开发工具
topic_type:
- apiref
api_name:
- TraceView -parsepdb
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86e176fc5e92cc7166c492ee8ebd2d63d3967040
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369653"
---
# <a name="traceview--parsepdb"></a>TraceView -parsepdb

使用**TraceView parsepdb**命令，以创建[跟踪消息格式文件](trace-message-format-file.md)中的数据从[PDB 符号文件](pdb-symbol-files.md)。

```
    traceview -parsepdb PDBfile [-p TMFPath] 
   
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______PDBfile______"></span><span id="_______pdbfile______"></span><span id="_______PDBFILE______"></span> *PDBfile*   
指定的 PDB 符号文件的路径和文件。

<span id="_______-p_______TMFPath______"></span><span id="_______-p_______tmfpath______"></span><span id="_______-P_______TMFPATH______"></span> **-p** *TMFPath*   
指定跟踪消息格式 (TMF) 文件的目录。

不能指定 TMF 文件的名称。 文件名称是[消息 GUID](message-guid.md)跟踪提供程序。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

```
traceview -parsepdb tracedrv.pdb
traceview -parsepdb tracedrv.pdb -p d:\tracing
```

备注

此外会创建 TraceView[跟踪消息控件 (.tmc) 文件](trace-message-control-file.md)每个[跟踪提供程序](trace-provider.md)的源代码中。 TMC 文件包含[控制 GUID](control-guid.md)和 PDB 文件中表示每个跟踪提供程序的跟踪级别。 TMC 文件的名称是控件的跟踪提供程序 GUID。

如果响应 TraceView **-parsepdb**命令仅通过显示**按任意键退出**消息，这可能表示所需的 DLL 不都已移到在其中的目录 TraceView可执行文件、 traceview.exe，所在。 有关详细信息，请参阅[准备使用 TraceView](preparing-to-use-traceview.md)。 这也可能表示 PDB 文件不具有所需的跟踪组件。 确认从其创建 PDB 文件的源代码已检测的软件跟踪。
