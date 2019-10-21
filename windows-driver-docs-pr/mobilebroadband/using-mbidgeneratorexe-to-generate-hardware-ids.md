---
title: 使用 mbidgenerator.exe 生成硬件 ID
description: 使用 mbidgenerator.exe 生成硬件 ID
ms.assetid: 2f2286e2-9300-4ef8-8e13-0851b60cd8eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96749ccbfa249efa6013812b67f95c9744c26747
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323653"
---
# <a name="using-mbidgeneratorexe-to-generate-hardware-ids"></a>使用 mbidgenerator.exe 生成硬件 ID

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

若要为服务元数据包生成硬件 ID 值，可以使用 MBIDGenerator 命令行工具，该工具是 SDK Windows 8.1 和 Windows 10 中的一部分。

**请    注意**，在 MBIDGenerator 中包含的是在 WDK 中包含的 Windows 8。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>送


MBIDGenerator 接受以下参数：

``` syntax
MBIDGenerator.exe [/Test] <input file> [<output file>]
```

**请注意**  *测试*参数提供非哈希输出，不应用于生成用于提交到 Windows 开发人员中心仪表板的硬件 id。

 

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>输出


MBIDGenerator 的输出通过标准命令行输出显示。 您也可以指定输出文件的路径和文件名。 错误始终报告回命令提示符。

输出值按以下方式显示：

``` syntax
<HardwareIDList>
  <HardwareID>MBAE:0:hashednumber1</HardwareID>
  <HardwareID>MBAE:0:hashednumber2</HardwareID>
  <HardwareID>MBAE:0:hashednumber3</HardwareID>
</HardwareIDList>
```

可以获取 MBIDGenerator 的输出，并将其插入服务元数据包的[PACKAGEINFO XML 架构](packageinfo-xml-schema.md)。

 

 





