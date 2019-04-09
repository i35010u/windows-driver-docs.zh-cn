---
title: ca
description: Ca 扩展显示控件区域有关的信息。
ms.assetid: 7e9164a5-238e-4327-bd2a-a814bff5f7db
keywords:
- 控件区域
- ca Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ca
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 329cbf608b047efc53ccf316e3d1af7a332c89a2
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238478"
---
# <a name="ca"></a>!ca


**！ Ca**扩展显示控件区域有关的信息。

```dbgsyntax
!ca [Address | 0 | -1] [Flags]
```

## <a name="span-idddkcadbgspanspan-idddkcadbgspanparameters"></a><span id="ddk__ca_dbg"></span><span id="DDK__CA_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
控件区域的地址。 如果指定此参数为 0，信息会显示有关所有控件区域。 如果指定此参数为-1，信息会显示有关未使用的段列表。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定所显示的信息的标志。 此参数是一个或多个下列标志的按位 OR。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="0x1"></span><span id="0X1"></span>0x1</p></td>
<td align="left"><p>显示段信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>显示子部分信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x4"></span><span id="0X4"></span>0x4</p></td>
<td align="left"><p>显示映射视图的列表。 (Windows 7 及更高版本)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x8"></span><span id="0X8"></span>0x8</p></td>
<td align="left"><p>显示压缩 （单行） 输出。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x10"></span><span id="0X10"></span>0x10</p></td>
<td align="left"><p>显示支持文件的控件区域。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x20"></span><span id="0X20"></span>0x20</p></td>
<td align="left"><p>显示控件区域由页面文件提供支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x40"></span><span id="0X40"></span>0x40</p></td>
<td align="left"><p>显示图像控件区域。</p></td>
</tr>
</tbody>
</table>

 

如果未指定任何的最后三个标志，将显示所有三种类型的控件区域。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关控制方面的信息，请参阅*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 

<a name="remarks"></a>备注
-------

若要获取的所有控件区域的列表映射文件，请使用[ **！ memusage** ](-memusage.md)扩展。

下面是一个示例：

```dbgcmd
kd> !memusage
 loading PFN database
loading (99% complete)
             Zeroed:     16 (    64 kb)
               Free:      0 (     0 kb)
            Standby:   2642 ( 10568 kb)
           Modified:    720 (  2880 kb)
    ModifiedNoWrite:      0 (     0 kb)
       Active/Valid:  13005 ( 52020 kb)
         Transition:      0 (     0 kb)
            Unknown:      0 (     0 kb)
              TOTAL:  16383 ( 65532 kb)
  Building kernel map
  Finished building kernel map

  Usage Summary (in Kb):
Control Valid Standby Dirty Shared Locked PageTables  name
ff8636e8    56    376     0     0     0     0  mapped_file( browseui.dll )
ff8cf388    24      0     0     0     0     0  mapped_file( AVH32DLL.DLL )
ff8d62c8    12      0     0     0     0     0  mapped_file( PSAPI.DLL )
ff8dd468   156     28     0     0     0     0  mapped_file( INOJOBSV.EXE )
fe424808   136     88     0    52     0     0  mapped_file( oleaut32.dll )
fe4228a8   152     44     0   116     0     0  mapped_file( MSVCRT.DLL )
ff8ec848     4      0     0     0     0     0    No Name for File
ff859de8     0     32     0     0     0     0  mapped_file( timedate.cpl )
. . . . .

kd> !ca ff8636e8

ControlArea @ff8636e8
  Segment:    e1b74548    Flink              0   Blink:               0
 Section Ref        0    Pfn Ref           6c   Mapped Views:        1
  User Ref           1    Subsections        5   Flush Count:         0
  File Object ff86df88    ModWriteCount      0   System Views:        0
  WaitForDel         0    Paged Usage      380   NonPaged Usage       e0
  Flags (10000a0) Image File HadUserReference 

   File: \WINNT\System32\browseui.dll

Segment @ e1b74548:
   Base address        0  Total Ptes        c8  NonExtendPtes:       c8
   Image commit        1  ControlArea ff8636e8  SizeOfSegment: c8000
   Image Base          0  Committed          0  PTE Template:   31b8438
 Based Addr   76e10000  ProtoPtes   e1b74580  Image Info:    e1b748a4

Subsection 1. @ ff863720
   ControlArea: ff8636e8  Starting Sector 0 Number Of Sectors 2
   Base Pte     e1b74580  Ptes In subsect        1 Unused Ptes          0
   Flags              15  Sector Offset          0 Protection           1
    ReadOnly CopyOnWrite 

Subsection 2. @ ff863740
   ControlArea: ff8636e8  Starting Sector 2 Number Of Sectors 3d0
   Base Pte     e1b74584  Ptes In subsect       7a Unused Ptes          0
   Flags              35  Sector Offset          0 Protection           3
    ReadOnly CopyOnWrite 

Subsection 3. @ ff863760
   ControlArea: ff8636e8  Starting Sector 3D2 Number Of Sectors 7
   Base Pte     e1b7476c  Ptes In subsect        1 Unused Ptes          0
   Flags              55  Sector Offset          0 Protection           5
    ReadOnly CopyOnWrite 

Subsection 4. @ ff863780
   ControlArea: ff8636e8  Starting Sector 3D9 Number Of Sectors 21f
   Base Pte     e1b74770  Ptes In subsect       44 Unused Ptes          0
   Flags              15  Sector Offset          0 Protection           1
    ReadOnly CopyOnWrite 

Subsection 5. @ ff8637a0
   ControlArea: ff8636e8  Starting Sector 5F8 Number Of Sectors 3a
   Base Pte     e1b74880  Ptes In subsect        8 Unused Ptes          0
   Flags              15  Sector Offset          0 Protection           1
    ReadOnly CopyOnWrite 
```

 

 





