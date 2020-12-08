---
title: .open（打开源文件）
description: "\"打开\" 命令在源路径中搜索源文件，并打开此文件。"
keywords:
- 。打开 (打开源文件) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .open (Open Source File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa680852ba98f4e1a39e444b60b4aab2e948b1d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811283"
---
# <a name="open-open-source-file"></a>.open（打开源文件）


" **打开** " 命令在源路径中搜索源文件，并打开此文件。

```dbgcmd
.open [-m Address] FileName 
.open -a Address 
```

## <a name="span-idddk_meta_open_source_file_dbgspanspan-idddk_meta_open_source_file_dbgspanparameters"></a><span id="ddk_meta_open_source_file_dbg"></span><span id="DDK_META_OPEN_SOURCE_FILE_DBG"></span>参数


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*FileName*   
指定源文件名称。 此名称可以包含绝对路径或相对路径。 除非指定绝对路径，否则，路径将被解释为相对于源路径中的目录。

<span id="_______-m_______Address______"></span><span id="_______-m_______address______"></span><span id="_______-M_______ADDRESS______"></span>**-m**  **** *地址*   
指定源文件中的地址。 此地址必须包含在已知的模块中。 如果文件名指定的文件不唯一，则应使用 **-m**  ****  *地址* 参数。 *FileName* 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

如果使用 [源服务器](using-a-source-server.md)检索源文件，则 **-m** 参数是必需的。

<span id="_______-a_______Address______"></span><span id="_______-a_______address______"></span><span id="_______-A_______ADDRESS______"></span>**-a** *地址*   
指定源文件中的地址。 此地址必须包含在已知的模块中。 如果调试器可以找到源文件，调试器将加载并打开该文件，并突出显示与指定地址对应的行。 如果调试器找不到源文件，则该地址将显示在 " [反汇编" 窗口](disassembly-window.md)中。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

只能在 WinDbg 中使用 " **打开** " 命令，而不能在脚本文件中使用它。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关源文件和源路径以及其他加载源文件的方式的详细信息，请参阅 [源路径](source-path.md)。

 

 





