---
title: PwrTest 日志文件
description: PwrTest 日志文件
ms.assetid: f4782b27-25e0-4ec3-bf0b-82a614815f90
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 186bc2b299b9480109c31656b9852c4372a4c1ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380963"
---
# <a name="pwrtest-log-file"></a>PwrTest 日志文件


PwrTest 以不同的格式支持多个同时进行日志记录输出：.log （纯文本）、.xml （格式因方案），.wtl (WTTLog) 和.etl （ETW 跟踪）。 默认情况下，PwrTest 生成名为 pwrtestlog 日志文件\*. 可以使用 **/ln:**<em>名称</em>选项可以更改日志名称。 默认情况下，将在当前目录中生成这些文件。 可以使用 **/lf:**<em>文件夹</em>选项来更改输出位置。

WTTLog 文件格式是普遍适用于 Microsoft Windows Driver Kit (WDK) 的所有工具的使用 WTTLog 接口。 如果不具有 WTTLog 安装在计算机上运行 PwrTest PwrTest 将不会生成.wtl (WTTLog) 日志文件。

PwrTest.xml 日志文件 (pwrtestlog.xml) 提供了有关运行时的特定方案的信息。 所有 PwrTest.xml 日志文件都具有以下根元素和标头：

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






