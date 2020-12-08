---
title: .imgscan（查找映像标头）
description: Imgscan 命令扫描图像标头的虚拟内存。
keywords:
- 查找图像标头 () 命令
- imgscan (查找) Windows 调试的图像标题
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .imgscan (Find Image Headers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8f62b27e9aca0c3ba98f54f7c43036d52acf761d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788963"
---
# <a name="imgscan-find-image-headers"></a>.imgscan（查找映像标头）


**Imgscan** 命令扫描图像标头的虚拟内存。

```dbgcmd
.imgscan [Options] 
```

## <a name="span-idddk_meta_find_image_headers_dbgspanspan-idddk_meta_find_image_headers_dbgspanparameters"></a><span id="ddk_meta_find_image_headers_dbg"></span><span id="DDK_META_FIND_IMAGE_HEADERS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下任意选项：

<span id="_r_Range"></span><span id="_r_range"></span><span id="_R_RANGE"></span>**/r**  **** *范围*  
指定要搜索的范围。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。 如果只指定一个地址，则调试器会搜索从该地址开始的范围，并扩展0x10000 字节。

<span id="_l"></span><span id="_L"></span>**/l**  
加载找到的任何图像标头的模块信息。

<span id="_v"></span><span id="_V"></span>**/v**  
显示详细信息。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

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

 

<a name="remarks"></a>备注
-------

如果不使用 **/r** 参数，调试器会搜索所有虚拟内存区域。

**Imgscan** 命令显示它找到的任何图像标头和标头类型。 标头类型包括可移植的可执行文件 (PE) 标头和 Microsoft MS-DOS MZ 标头。

下面的示例演示了 **imgscan** 命令。

```dbgcmd
0:000> .imgscan
MZ at 00400000, prot 00000002, type 01000000 - size 2d000
MZ at 77f80000, prot 00000002, type 01000000 - size 7d000
  Name: ntdll.dll
MZ at 7c570000, prot 00000002, type 01000000 - size b8000
  Name: KERNEL32.dll
```

 

 





