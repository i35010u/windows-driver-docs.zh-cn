---
title: .enumtag （辅助回调数据枚举）
description: .Enumtag 命令显示辅助 bug 检查回调数据和所有数据标记。
ms.assetid: 2146ebb9-96ce-4eb0-8c23-c9aaa5ed7f73
keywords:
- .enumtag （辅助回调数据枚举） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .enumtag (Enumerate Secondary Callback Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9987446b2e863e298d6a223b1533185ade168aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547732"
---
# <a name="enumtag-enumerate-secondary-callback-data"></a>.enumtag （辅助回调数据枚举）


**.Enumtag**命令显示辅助 bug 检查回调数据和所有数据标记。

```dbgcmd
.enumtag 
```

## <span id="ddk_meta_enumerate_secondary_callback_data_dbg"></span><span id="DDK_META_ENUMERATE_SECONDARY_CALLBACK_DATA_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
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

有关详细信息以及有关显示此数据的其他方法，请参阅[读取 Bug 检查回调数据](reading-bug-check-callback-data.md)。

<a name="remarks"></a>备注
-------

可以使用 **.enumtag**命令仅发生的 bug 检查后或在调试时的内核模式崩溃转储文件。

对于每个辅助 bug 块检查回调数据 **.enumtag**命令显示了 （采用 GUID 格式） 的标记和数据 （作为 ASCII 字符和字节）。

请考虑下面的示例。

```dbgcmd
kd> .enumtag
{87654321-0000-0000-0000000000000000} - 0xf9c bytes
  4D 5A 90 00 03 00 00 00 04 00 00 00 FF FF 00 00  MZ..............
  B8 00 00 00 00 00 00 00 40 00 00 00 00 00 00 00  ........@.......
  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
  ....
  00 00 00 00 00 00 00 00 00 00 00 00              ............

{12345678-0000-0000-0000000000000000} - 0x298 bytes
  F4 BF 7B 80 F4 BF 7B 80 00 00 00 00 00 00 00 00  ..{...{.........
 4B 44 42 47 98 02 00 00 00 20 4D 80 00 00 00 00  KDBG..... M.....
  54 A5 57 80 00 00 00 00 A0 50 5A 80 00 00 00 00  T.W......PZ.....
 40 01 08 00 18 00 00 00 BC 7D 50 80 00 00 00 00  @........}P.....
  ....
  00 00 00 00 00 00 00 00                          ........
```

在此示例中，辅助数据的第一批都有一个 GUID）{87654321-0000-0000-0000000000000000}) 为相应的标记，第二个批处理的数据都有一个 GUID ({12345678-0000-0000-0000000000000000}) 为其标记。 但是，数据不是以有用的格式。

 

 





