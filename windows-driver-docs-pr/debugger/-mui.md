---
title: 界面
description: Mui 扩展显示多语言用户界面 (MUI) 缓存信息。 MUI 的实现在 Windows Vista 中已改进。
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
ms.openlocfilehash: 9f8c9b0585af8e466e8e18ccfb5caaebd5d12c0f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790101"
---
# <a name="mui"></a>!mui


**！ Mui** 扩展显示多语言用户界面 (mui) 缓存信息。 

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

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-c______"></span><span id="_______-C______"></span>**-c**   
使输出包含语言标识符 (ID) 、指向模块的指针、指向资源配置数据的指针，以及指向每个模块的关联 MUI DLL 的指针。

<span id="_______-s______"></span><span id="_______-S______"></span>**-s**   
仅 (内核模式) 导致显示包含模块的完整文件路径以及每个模块的关联 MUI DLL。

<span id="_______-r________ModuleAddress______"></span><span id="_______-r________moduleaddress______"></span><span id="_______-R________MODULEADDRESS______"></span>**-r**  **** *ModuleAddress*   
使 *ModuleAddress* 的模块的资源配置数据显示。 这包括文件类型、校验和值以及资源类型。

<span id="_______-i______"></span><span id="_______-I______"></span>**-i**   
导致输出包含已安装的和许可的 MUI 语言及其关联的信息。

<span id="_______-f______"></span><span id="_______-F______"></span>**-f**   
导致输出包含加载程序合并语言回退列表。

<span id="_______-t______"></span><span id="_______-T______"></span>**-t**   
导致输出包含线程首选项。

<span id="_______-u______"></span><span id="_______-U______"></span>**-u**   
导致输出包含当前线程用户 UI 语言设置。

<span id="_______-d_ModuleAddress______"></span><span id="_______-d_moduleaddress______"></span><span id="_______-D_MODULEADDRESS______"></span>**-d**  **** *ModuleAddress*   
导致输出在 *ModuleAddress* 中包含模块的包含资源。

<span id="_______-e_ModuleAddress______"></span><span id="_______-e_moduleaddress______"></span><span id="_______-E_MODULEADDRESS______"></span>**-e**  **** *ModuleAddress*   
导致输出在 *ModuleAddress* 中包含模块的包含资源类型。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简短帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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
<td align="left"><p><strong>Windows Vista 及更高版本</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 MUI 和资源配置数据格式的信息，请参阅 Microsoft Windows SDK 文档。

 

 





