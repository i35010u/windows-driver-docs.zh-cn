---
title: wdfkd.wdfsearchpath
description: Wdfkd.wdfsearchpath 扩展设置格式设置为内核模式驱动程序框架 (KMDF) 错误日志记录的文件的搜索路径。
ms.assetid: cb52dc07-00b3-47d3-8636-4a6cd5ff3e29
keywords:
- wdfkd.wdfsearchpath Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfsearchpath
api_location:
- Wdfkd.dll
api_type:
- DllExport
ms.localizationpriority: medium
ms.openlocfilehash: ccf2ce7ca4ac573a2fd419ef2ae9630f7226983b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564261"
---
# <a name="wdfkdwdfsearchpath"></a>!wdfkd.wdfsearchpath


**！ Wdfkd.wdfsearchpath**扩展格式设置为内核模式驱动程序框架 (KMDF) 错误日志记录的文件设置的搜索路径。

```dbgcmd
!wdfkd.wdfsearchpath Path
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *路径*   
包含 KMDF 格式设置文件的目录的路径。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架


KMDF 1，UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

KMDF 格式设置文件包含 Windows Driver Kit (WDK) 中。 格式设置文件的路径取决于你 WDK 的安装目录和已安装 WDK 的版本。 KMDF 格式设置文件具有扩展名 tmf （跟踪消息格式）。 若要确定搜索路径，请浏览或搜索 WDK 安装的文件名称的窗体 Wdf*VersionNumber*.tmf。 下面的示例演示如何使用 **！ wdfkd.wdfsearchpath**扩展。

```dbgcmd
kd> !wdfsearchpath C:\WinDDK\7600\tools\tracing\amd64
```

跟踪\_格式\_搜索\_PATH 环境变量还可以控制搜索路径中，但 **！ wdfkd.wdfsearchpath**扩展的优先级高于搜索路径的跟踪\_格式\_搜索\_路径指定。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">Wdfkd.dll</td>
</tr>
</tbody>
</table>

 

 





