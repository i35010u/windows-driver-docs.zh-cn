---
title: .open（打开源文件）
description: 打开命令将搜索源文件的源路径，并打开此文件。
ms.assetid: 49944fc8-5ecb-47a4-a046-0df18a242e72
keywords:
- 打开 （开放源代码文件） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .open (Open Source File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef67ba926a5c6612c7dc30f9281a916b91751788
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334421"
---
# <a name="open-open-source-file"></a>.open（打开源文件）


**打开**命令将搜索源文件的源路径，并打开此文件。

```dbgcmd
.open [-m Address] FileName 
.open -a Address 
```

## <a name="span-idddkmetaopensourcefiledbgspanspan-idddkmetaopensourcefiledbgspanparameters"></a><span id="ddk_meta_open_source_file_dbg"></span><span id="DDK_META_OPEN_SOURCE_FILE_DBG"></span>参数


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
指定源文件的名称。 此名称可以包含绝对或相对路径。 除非指定绝对路径，路径被解释为相对于源路径中的目录。

<span id="_______-m_______Address______"></span><span id="_______-m_______address______"></span><span id="_______-M_______ADDRESS______"></span> **-m** **** *Address*   
指定在源文件中的地址。 此地址必须包含在一个已知的模块。 应使用 **-m** **** *地址*参数如果该文件的*FileName*指定不是唯一的。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

**-M**参数是必需的如果使用的[源服务器](using-a-source-server.md)检索源文件。

<span id="_______-a_______Address______"></span><span id="_______-a_______address______"></span><span id="_______-A_______ADDRESS______"></span> **-a** *Address*   
指定在源文件中的地址。 此地址必须包含在一个已知的模块。 如果调试器可以找到的源文件，调试器将加载并打开该文件，并突出显示对应于指定的地址的行。 如果调试器无法找到的源文件，该地址将显示在[反汇编窗口](disassembly-window.md)。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

可以使用**打开**命令仅在 WinDbg 中，并且您不能在脚本文件中使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关源的文件和源路径的详细信息并加载源文件的其他方法，请参阅[源路径](source-path.md)。

 

 





