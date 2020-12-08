---
title: dskheap
description: Dskheap 扩展显示指定会话的桌面堆信息。
keywords:
- 电脑
- dskheap Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dskheap
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 44f8ec109137eebd0493e30aa88bf599a94df0ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796343"
---
# <a name="dskheap"></a>!dskheap


**！ Dskheap** extension 显示指定会话的桌面堆信息。

```dbgcmd
!dskheap [-v] [-s SessionID]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
使显示包含更详细的输出。

<span id="_______-s_SessionID"></span><span id="_______-s_sessionid"></span><span id="_______-S_SESSIONID"></span>**-s**  **** *SessionID*  
指定一个会话。 如果省略此参数，则将显示会话0的桌面堆信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>



### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关桌面或桌面堆的信息，请参阅 Russinovich 文档和 *Microsoft Windows 内部机制* ，并将 Microsoft Windows SDK 其标记为和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

会话的桌面堆信息按窗口工作站排列。

下面是几个示例：

```dbgcmd
kd> !dskheap -s 3
##   Winstation\Desktop            Heap Size(KB)   Used Rate(%)

  WinSta0\Screen-saver              3072                 0%
  WinSta0\Default                   3072                 0%
  WinSta0\Disconnect                  64                 4%
##   WinSta0\Winlogon                   128                 5%

                Total Desktop: (    6336 KB -   4 desktops)
#                 Session ID:  3

kd> !dskheap
##   Winstation\Desktop            Heap Size(KB)   Used Rate(%)

  WinSta0\Default                   3072                 0%
  WinSta0\Disconnect                  64                 4%
  WinSta0\Winlogon                   128                 9%
  Service-0x0-3e7$\Default           512                 4%
  Service-0x0-3e5$\Default           512                 0%
  Service-0x0-3e4$\Default           512                 1%
##   SAWinSta\SADesktop                 512                 0%

                Total Desktop: (    5312 KB -   7 desktops)
#                 Session ID:  0
```









