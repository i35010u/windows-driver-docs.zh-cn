---
title: wdfkd.wdfsearchpath
description: Wdfkd wdfsearchpath 扩展设置 Kernel-Mode Driver Framework (KMDF) 错误日志记录的格式设置文件的搜索路径。
keywords:
- wdfkd wdfsearchpath Windows 调试
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
ms.openlocfilehash: c2e6bc35e6d05ed775827362037c0acfe0e3dfbd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802025"
---
# <a name="wdfkdwdfsearchpath"></a>!wdfkd.wdfsearchpath


**！ Wdfkd wdfsearchpath** 将 Kernel-Mode Driver FRAMEWORK (KMDF) 错误日志记录的格式设置文件的搜索路径。

```dbgcmd
!wdfkd.wdfsearchpath Path
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span>*路径*   
包含 KMDF 格式设置文件的目录的路径。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作


KMDF 1，UMDF 2

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

KMDF 格式设置文件包含在 (WDK) 的 Windows 驱动程序工具包中。 格式设置文件的路径取决于 WDK 的安装目录以及已安装的 WDK 版本。 KMDF 格式设置文件具有扩展名 tmf (跟踪消息格式) 。 若要确定搜索路径，请浏览或搜索你的 WDK 安装，查找格式为 Wdf *VersionNumber*. tmf 的文件名。 下面的示例演示如何使用 **！ wdfkd. wdfsearchpath** 扩展。

```dbgcmd
kd> !wdfsearchpath C:\WinDDK\7600\tools\tracing\amd64
```

跟踪 \_ 格式 \_ 搜索 \_ 路径环境变量还控制搜索路径，但 **！ wdfkd wdfsearchpath** 扩展的优先级高于跟踪 \_ 格式 \_ 搜索路径指定的搜索路径 \_ 。

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

 

 





