---
title: 使用 mbidgenerator.exe 生成硬件 ID
description: 使用 mbidgenerator.exe 生成硬件 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1a57d240f0c1a40182e5f0d69fe8ef8e0ba2c6d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783847"
---
# <a name="using-mbidgeneratorexe-to-generate-hardware-ids"></a>使用 mbidgenerator.exe 生成硬件 ID

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

若要为服务元数据包生成硬件 ID 值，可以使用 MBIDGenerator.exe 命令行工具，该工具在 Windows 8.1 和 Windows 10 中是 SDK 的一部分。

**注意**  
在 Windows 8 中，MBIDGenerator.exe 包含在 WDK 中。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>送


MBIDGenerator.exe 接受以下参数：

``` syntax
MBIDGenerator.exe [/Test] <input file> [<output file>]
```

**注意**  
*Test* 参数提供非哈希输出，不应用于生成用于提交到 Windows 开发人员中心仪表板的硬件 id。

 

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>输出


MBIDGenerator.exe 的输出是通过标准命令行输出显示的。 您也可以指定输出文件的路径和文件名。 错误始终报告回命令提示符。

输出值按以下方式显示：

``` syntax
<HardwareIDList>
  <HardwareID>MBAE:0:hashednumber1</HardwareID>
  <HardwareID>MBAE:0:hashednumber2</HardwareID>
  <HardwareID>MBAE:0:hashednumber3</HardwareID>
</HardwareIDList>
```

可以从 MBIDGenerator.exe 获取输出，并将其插入服务元数据包的 [PACKAGEINFO XML 架构](packageinfo-xml-schema.md) 。

 

 





