---
title: .enumtag（枚举辅助回调数据）
description: Enumtag 命令显示辅助 bug 检查回调数据和所有数据标记。
keywords:
- enumtag (枚举辅助回调数据) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .enumtag (Enumerate Secondary Callback Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1404ad86820c4a25be6648bd676fd96727bb2949
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785315"
---
# <a name="enumtag-enumerate-secondary-callback-data"></a>.enumtag（枚举辅助回调数据）


**Enumtag** 命令显示辅助 bug 检查回调数据和所有数据标记。

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
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
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

有关详细信息和显示此数据的其他方式，请参阅 [读取 Bug 检查回调数据](reading-bug-check-callback-data.md)。

<a name="remarks"></a>备注
-------

仅在发生了 bug 检查或调试内核模式故障转储文件后，才能使用 **enumtag** 命令。

对于每个辅助 bug 检查回调数据块， **enumtag** 命令将以 GUID 格式显示标记 () 并将数据 (为字节，并) ASCII 字符。

请看下面的示例。

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

在此示例中，第一批辅助数据的 {87654321-0000-0000-0000000000000000} 标记) 为 guid ) ，第二批数据的 guid ({12345678-0000-0000-0000000000000000}) 作为其标记。 但数据的格式不是很有用。

 

 





