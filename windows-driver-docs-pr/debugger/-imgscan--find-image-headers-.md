---
title: .imgscan（查找映像标头）
description: .Imgscan 命令扫描映像标头的虚拟内存。
ms.assetid: 8b524665-0471-4634-aa31-1c82d6cc8569
keywords:
- 查找映像标头 (.imgscan) 命令
- .imgscan （查找映像标头） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .imgscan (Find Image Headers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 92a77a5c6c481736380f411e2c8659941746b41d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336426"
---
# <a name="imgscan-find-image-headers"></a>.imgscan（查找映像标头）


**.Imgscan**命令扫描映像标头的虚拟内存。

```dbgcmd
.imgscan [Options] 
```

## <a name="span-idddkmetafindimageheadersdbgspanspan-idddkmetafindimageheadersdbgspanparameters"></a><span id="ddk_meta_find_image_headers_dbg"></span><span id="DDK_META_FIND_IMAGE_HEADERS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下任意选项：

<span id="_r_Range"></span><span id="_r_range"></span><span id="_R_RANGE"></span>**/r** **** *范围*  
指定要搜索的范围。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。 指定只能有一个地址时，调试器将搜索该地址处开头并扩展了 0x10000 字节的范围。

<span id="_l"></span><span id="_L"></span>**/l**  
加载模块位于任何映像标头信息。

<span id="_v"></span><span id="_V"></span>**/v**  
显示详细的信息。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

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

 

<a name="remarks"></a>备注
-------

如果不使用 **/r**参数，调试器将搜索所有的虚拟内存区域。

**.Imgscan**命令显示它找到任何映像标头和标头类型。 标头类型包括可移植可执行文件 (PE) 标头和 Microsoft MS-DOS MZ 标头。

下面的示例演示 **.imgscan**命令。

```dbgcmd
0:000> .imgscan
MZ at 00400000, prot 00000002, type 01000000 - size 2d000
MZ at 77f80000, prot 00000002, type 01000000 - size 7d000
  Name: ntdll.dll
MZ at 7c570000, prot 00000002, type 01000000 - size b8000
  Name: KERNEL32.dll
```

 

 





