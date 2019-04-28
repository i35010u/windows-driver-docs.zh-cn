---
title: dskheap
description: Dskheap 扩展显示指定的会话的桌面堆信息。
ms.assetid: e49c816f-963c-4383-a3bf-c03b2c0cfa39
keywords:
- desktops
- dskheap Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dskheap
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 55c3f4b6f9bfc773e2ade5f939ab2cc414980191
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334532"
---
# <a name="dskheap"></a>!dskheap


**！ Dskheap**扩展将显示指定的会话的桌面堆信息。

```dbgcmd
!dskheap [-v] [-s SessionID]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
将导致显示以包括更详细的输出。

<span id="_______-s_SessionID"></span><span id="_______-s_sessionid"></span><span id="_______-S_SESSIONID"></span> **-s** **** *SessionID*  
指定的会话。 如果省略此参数，则会显示用于 session 0 的桌面堆信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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



### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关桌面或桌面堆的信息，请参阅 Microsoft Windows SDK 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

会话的桌面堆信息排列的窗口区域。

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









