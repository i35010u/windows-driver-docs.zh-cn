---
title: mui
description: Mui 扩展显示的多语言用户界面 (MUI) 缓存信息。 Windows Vista 中改进了 MUI 的实现。
ms.assetid: f485450f-0dd2-4f1c-85fe-dbf272c2dbae
keywords:
- 多语言用户界面
- mui Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- mui
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ea2ef45f04ede7e83ae51252ca7cffb655da1f88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336036"
---
# <a name="mui"></a>!mui


**！ Mui**扩展显示的多语言用户界面 (MUI) 缓存信息。 

```dbgcmd
!mui -c
!mui -s
!mui -r ModuleAddress
!mui -i
!mui -f
!mui -t
!mui -u
!mui -d ModuleAddress
!mui -e ModuleAddress
!mui -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
会使包含语言标识符 (ID)、 指向模块的指针、 指向资源配置数据的指针和指向关联的 MUI DLL，为每个模块的输出。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
（仅适用于内核模式）将导致显示以包括该模块的完整文件路径和每个模块关联的 MUI DLL。

<span id="_______-r________ModuleAddress______"></span><span id="_______-r________moduleaddress______"></span><span id="_______-R________MODULEADDRESS______"></span> **-r** **** *ModuleAddress*   
在模块的资源配置数据将导致*ModuleAddress*显示。 这包括的文件类型、 校验和值和资源类型。

<span id="_______-i______"></span><span id="_______-I______"></span> **-i**   
会导致输出包含已安装和许可 MUI 语言和与其相关的信息。

<span id="_______-f______"></span><span id="_______-F______"></span> **-f**   
会导致输出包括加载程序合并的语言回退列表。

<span id="_______-t______"></span><span id="_______-T______"></span> **-t**   
会导致输出包括线程的首选语言。

<span id="_______-u______"></span><span id="_______-U______"></span> **-u**   
会导致输出包含当前线程用户 UI 语言设置。

<span id="_______-d_ModuleAddress______"></span><span id="_______-d_moduleaddress______"></span><span id="_______-D_MODULEADDRESS______"></span> **-d** **** *ModuleAddress*   
输出包含在模块包含的资源将导致*ModuleAddress*。

<span id="_______-e_ModuleAddress______"></span><span id="_______-e_moduleaddress______"></span><span id="_______-E_MODULEADDRESS______"></span> **-e** **** *ModuleAddress*   
导致要包括的模块在包含的资源类型的输出*ModuleAddress*。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简要帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows Vista 及更高版本</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 MUI 和资源配置数据格式的信息，请参阅 Microsoft Windows SDK 文档。

 

 





