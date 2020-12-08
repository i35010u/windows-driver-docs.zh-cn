---
title: PwrTest 平台空闲方案
description: PwrTest 平台空闲方案 (/platidle) 轮询，并尝试记录平台空闲转换计数（如果计算机支持）。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d013e8a0ea08a5b8612987f9243f7b6d290a790
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823363"
---
# <a name="pwrtest-platform-idle-scenario"></a>PwrTest 平台空闲方案


PwrTest 平台空闲方案 (**/platidle**) 轮询，并尝试记录平台空闲转换计数（如果计算机支持）。

此方案有助于跟踪在计算机使用时发生的平台空闲状态转换。 此方案还有助于诊断系统是否进入深层平台空闲状态 (如果是通过 "电源" 按钮) 手动输入的。

**/Platidle** 方案要求计算机支持 *alwayson Always 连接* (AoAc) 功能。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /platidle  [/t:n] [/i:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t：**<em>n</em>  
指定运行该方案 (默认 *值为 30* 分钟) )  (的总时间（分钟）。

<span id="_i_n"></span><span id="_I_N"></span>**/i：**<em>n</em>  
指定轮询间隔 (秒) 用于收集平台空闲统计信息 (*n* 的默认值为5秒) 。

**示例**

```
pwrtest /platidle /t:60
```

```
pwrtest /platidle
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <PlatIdle> 
    <PlatformIdleStats StateCount="X" Timestamp="XX/XX/XXXX:XX:XX:XX.XXX">
        <State Index="X" SuccessCount="X" FailureCount="X" CancelCount="X"/>
    </PlatformIdleStats>
  </PlatIdle>
</PwrTestLog> 
```

下表描述了日志文件中显示的 XML 元素。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">元素</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>&lt;PlatIdle&gt;</strong></td>
<td align="left"><p>包含所有平台空闲统计信息。 PwrTest 日志文件中只有一个<strong> &lt; PlatIdle &gt; </strong>元素</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PlatformIdleStats&gt;</strong></td>
<td align="left"><p>平台空闲统计信息块。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






