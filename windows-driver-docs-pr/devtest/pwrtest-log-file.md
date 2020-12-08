---
title: PwrTest 日志文件
description: PwrTest 日志文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9768461968593390807cc6af7cf2ca9de74e0833
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824605"
---
# <a name="pwrtest-log-file"></a>PwrTest 日志文件


PwrTest 支持不同格式的多个同时进行的日志记录输出： .log (纯文本) 、.xml (格式因应用场景而异) ，. wtl (WTTLog) 和 .etl (ETW 跟踪) 。 默认情况下，PwrTest 生成名为 \* pwrtestlog 的日志文件。 可以使用 **/ln：**<em>name</em> 选项更改日志名称。 默认情况下，将在当前目录中生成这些文件。 可以使用 **/lf：**<em>folder</em> 选项更改输出位置。

WTTLog 文件格式适用于所有 Microsoft Windows 驱动程序工具包 (WDK) 使用 WTTLog 接口的工具。 如果在未安装 WTTLog 的计算机上运行 PwrTest，PwrTest 不会生成 wtl (WTTLog) 日志文件。

PwrTest 日志文件 ( # A0) 提供有关运行的特定方案的信息。 所有 PwrTest 日志文件都具有以下根元素和标头：

```XML
<PwrTestLog date="today's date" time="beginning time" filename = "logfile path">
  <SystemInformation>
    <ComputerName></ComputerName>
    <OSBuildNumber></OSBuildNumber>
    <SystemManufacturer></SystemManufacturer>
    <SystemProductName></SystemProductName>
    <BIOSVersion></BIOSVersion>
    <BIOSReleaseDate></BIOSReleaseDate>
    <ProcessorCount></ProcessorCount>
    <ProcessorPackageCount></ProcessorPackageCount>
  </SystemInformation>

  ... 
  scenario tags and data
  ...

</PwrTestLog>
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






