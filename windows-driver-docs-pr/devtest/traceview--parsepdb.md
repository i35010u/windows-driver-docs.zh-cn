---
title: TraceView -parsepdb
description: 使用 TraceView-parsepdb 命令从 PDB 符号文件中的数据创建跟踪消息格式文件。
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
ms.openlocfilehash: 8c311b174dd8fb190290fa052aa51dd126df32cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838111"
---
# <a name="traceview--parsepdb"></a>TraceView -parsepdb

使用 **TraceView-parsepdb** 命令从 [PDB 符号文件](pdb-symbol-files.md)中的数据创建 [跟踪消息格式文件](trace-message-format-file.md)。

```
    traceview -parsepdb PDBfile [-p TMFPath] 
   
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______PDBfile______"></span><span id="_______pdbfile______"></span><span id="_______PDBFILE______"></span>*PDBfile*   
指定 PDB 符号文件的路径和文件名。

<span id="_______-p_______TMFPath______"></span><span id="_______-p_______tmfpath______"></span><span id="_______-P_______TMFPATH______"></span>**-p** *TMFPath*   
指定跟踪消息格式 (TMF) 文件的目录。

不能指定 TMF 文件的名称。 文件名为跟踪提供程序的 [消息 GUID](message-guid.md) 。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

```
traceview -parsepdb tracedrv.pdb
traceview -parsepdb tracedrv.pdb -p d:\tracing
```

注释

TraceView 还会为源代码中的每个[跟踪提供程序](trace-provider.md)创建[跟踪消息控制 ( tmc) 文件](trace-message-control-file.md)。 TMC 文件包含 PDB 文件中表示的每个跟踪提供程序的 [控件 GUID](control-guid.md) 和跟踪级别。 TMC 文件的名称为跟踪提供程序的控件 GUID。

如果 TraceView 只通过显示 "**按任意键退出** 消息" 来响应 **-parsepdb** 命令，则这可能表示所需的 DLL 尚未移到 TraceView 可执行文件 traceview.exe 的目录中。 有关详细信息，请参阅 [准备使用 TraceView](preparing-to-use-traceview.md)。 这也可能表示 PDB 文件没有所需的跟踪组件。 确认为软件跟踪检测了从中创建了 PDB 文件的源代码。
