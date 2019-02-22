---
title: PwrTest 平台空闲方案
description: PwrTest 平台空闲方案 (/ platidle) 轮询，并尝试登录平台空闲转换计数，如果计算机支持。
ms.assetid: 71A3AB26-AAC5-46DB-99A3-6693D5AF5AC9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c2a477c5a1ff8ad446ac8bdee6aeaa9238345b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554815"
---
# <a name="pwrtest-platform-idle-scenario"></a>PwrTest 平台空闲方案


PwrTest 平台空闲方案 (**/platidle**) 轮询，并尝试登录平台空闲转换计数，如果计算机支持。

此方案可用于跟踪计算机正在使用中时出现的平台闲置状态转换。 这种情况下还可以帮助诊断如果系统正在进入深入的平台空闲状态 （如果通过电源按钮手动输入）。

**/Platidle**方案要求计算机具有支持*始终打开始终连接*(AoAc) 电源功能。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


```
pwrtest /platidle  [/t:n] [/i:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
为方案运行指定的总时间 （以分钟为单位） (默认值*n*为 30 分钟)。

<span id="_i_n"></span><span id="_I_N"></span>**/i:**<em>n</em>  
指定轮询间隔 （以秒为单位） 为收集平台空闲统计信息 (默认值*n*为 5 秒)。

**示例**

```
pwrtest /platidle /t:60
```

```
pwrtest /platidle
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML 日志文件输出

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

下表介绍日志文件中显示的 XML 元素。

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
<td align="left"><p>包含所有平台空闲统计信息。 只有一个<strong>&lt;PlatIdle&gt;</strong> PwrTest 日志文件中的元素</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PlatformIdleStats&gt;</strong></td>
<td align="left"><p>平台空闲状态的统计信息块。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[PwrTest 语法](pwrtest-syntax.md)

 

 






