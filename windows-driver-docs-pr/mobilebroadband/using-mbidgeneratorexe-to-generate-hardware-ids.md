---
title: 使用 mbidgenerator.exe 生成硬件 Id
description: 使用 mbidgenerator.exe 生成硬件 Id
ms.assetid: 2f2286e2-9300-4ef8-8e13-0851b60cd8eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96749ccbfa249efa6013812b67f95c9744c26747
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547924"
---
# <a name="using-mbidgeneratorexe-to-generate-hardware-ids"></a>使用 mbidgenerator.exe 生成硬件 Id

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

若要生成你的服务元数据包的硬件 ID 值，可以使用 MBIDGenerator.exe 命令行工具，它是在 Windows 8.1 和 Windows 10 SDK 的一部分。

**请注意**   WDK 中已包含在 Windows 8 MBIDGenerator.exe。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>输入


MBIDGenerator.exe 接受以下参数：

``` syntax
MBIDGenerator.exe [/Test] <input file> [<output file>]
```

**请注意**   *测试*参数提供非哈希处理的输出，不应该用于生成硬件 Id 以提交到 Windows 开发人员中心仪表板。

 

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>Output


MBIDGenerator.exe 的输出是通过标准命令行输出显示。 或者，可以指定输出文件的路径和文件名称。 在命令提示符下，将始终返回报告错误。

按以下方式显示的输出值：

``` syntax
<HardwareIDList>
  <HardwareID>MBAE:0:hashednumber1</HardwareID>
  <HardwareID>MBAE:0:hashednumber2</HardwareID>
  <HardwareID>MBAE:0:hashednumber3</HardwareID>
</HardwareIDList>
```

你可以从 MBIDGenerator.exe 采取输出并将其插入到[PackageInfo XML 架构](packageinfo-xml-schema.md)的在服务元数据包。

 

 





