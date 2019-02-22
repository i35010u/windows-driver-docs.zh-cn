---
title: filecache
description: Filecache 扩展显示有关系统文件缓存内存和 PTE 使用的信息。
ms.assetid: 38dbff14-5144-455c-a9b8-1ac6292f4200
keywords:
- 文件缓存
- filecache Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- filecache
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 494d76d1cb348f9018dd75b693306d2e63b8e5ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519710"
---
# <a name="filecache"></a>！ filecache


**！ Filecache**扩展显示有关系统文件缓存内存的信息，并使用 PTE。

```dbgcmd
!filecache [Flags]
```

## <a name="span-idddkfilelockdbgspanspan-idddkfilelockdbgspanparameters"></a><span id="ddk__filelock_dbg"></span><span id="DDK__FILELOCK_DBG"></span>参数


<span id="_______Flags"></span><span id="_______flags"></span><span id="_______FLAGS"></span> *标志*  
可选。 默认值为 0x0。 设置*标志*为 0x1 的输出进行排序由共享的缓存映射。 这种方式可以找到给定的控件区域的所有系统缓存视图。

## <span id="ddk__filecache_dbg"></span><span id="DDK__FILECACHE_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

文件系统驱动程序有关的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

此扩展的输出的每一行表示虚拟地址控制块 (VACB)。 当命名的文件映射到 VACB 时，显示这些文件的名称。 如果指定"没有的文件名称"，这意味着此 VACB 使用缓存元数据。

下面是输出的从 Windows XP 系统中此扩展示例：

```dbgcmd
kd> !filecache
***** Dump file cache******
  Reading and sorting VACBs ...
  Removed 1811 nonactive VACBs, processing 235 active VACBs ...
File Cache Information
  Current size 28256 kb
  Peak size    30624 kb
  235 Control Areas
Skipping view @ c1040000 - no VACB, but PTE is valid!
  Loading file cache database (100% of 131072 PTEs)
  SkippedPageTableReads = 44
  File cache has 4056 valid pages
 

  Usage Summary (in Kb):
Control Valid Standby/Dirty Shared Locked Name
817da668     4      0     0     0  $MftMirr
8177ae68   304    920     0     0  $LogFile
81776160   188      0     0     0  $BitMap
817cf370     4      0     0     0  $Mft
81776a00     8      0     0     0  $Directory
817cfdd0     4      0     0     0  $Directory
81776740    36      0     0     0    No Name for File
817cf7c8    20      0     0     0  $Directory
817cfb98   304      0     0     0  $Directory
8177be40    16      0     0     0  $Directory
817dadc0  2128     68     0     0  $Mft
817cf008     4      0     0     0  $Directory
817d0258     8      4     0     0  $Directory
817763f8     4      0     0     0  $Directory
...
8173f058     4      0     0     0  $Directory
8173e628    32      0     0     0  $Directory
8173e4c8    32      0     0     0  $Directory
8173da38     4      0     0     0  $Directory
817761f8     4      0     0     0  $Directory
81740530    32      0     0     0  $Directory
8173d518     4      0     0     0  $Directory
817d9560     8      0     0     0  $Directory
8173f868     4      0     0     0  $Directory
8173fc00     4      0     0     0  $Directory
81737278     4      0     0     0  $MftMirr
81737c88    44      0     0     0  $LogFile
81735fa0    48      0     0     0  $Mft
81737e88   188      0     0     0  $BitMap
817380b0     4      0     0     0  $Mft
817399e0     4      0     0     0  $Directory
817382b8     4      0     0     0  $Directory
817388d8    12      0     0     0    No Name for File
81735500     8      0     0     0  $Directory
81718e38   232      0     0     0  default
81735d40    48     20     0     0  SECURITY
81723008  8632      0     0     0  software
816da3a0    24     44     0     0  SAM
8173dfa0     4      0     0     0  $Directory
...
8173ba90     4      0     0     0  $Directory
8170ee30     4     36     4     0  AppEvent.Evt
816223f8     4      0     0     0  $Directory
8170ec28     8     28     4     0  SecEvent.Evt
816220a8     4      0     0     0  $Directory
8170ea20     4     32     4     0  SysEvent.Evt
8170d188   232      0     0     0  NTUSER.DAT
81709f10     8      0     0     0  UsrClass.dat
81708918   232      0     0     0  NTUSER.DAT
81708748     8      0     0     0  UsrClass.dat
816c58f8    12      0     0     0  change.log
815c3880     4      0     0     0  $Directory
81706aa8     4      0     0     0  SchedLgU.Txt
815ba2d8     4      0     0     0  $Directory
815aa5f8     8      0     0     0  $Directory
8166d728    44      0     0     0  Netlogon.log
81701120     8     16     4     0  es.dll
816ff0a8     4      8     4     0  stdole2.tlb
8159a358     4      0     0     0  $Directory
8159da70     4      0     0     0  $Directory
8159c158     4      0     0     0  $Directory
815cb9b0     4      0     0     0  00000001
81779b20     4      0     0     0  $Directory
8159ac20     4      0     0     0  $Directory
815683f8     4      0     0     0  $Directory
81566978   580      0     0     0  NTUSER.DAT
81568460     4      0     0     0  $Directory
815675d8    68      0     0     0  UsrClass.dat
81567640     4      0     0     0  $Directory
...
81515878     4      0     0     0  $Directory
81516870     8      0     0     0  $Directory
8150df60     4      0     0     0  $Directory
...
816e5300     4      0     0     0  $Directory
8152afa0    16    212     0     0  msmsgs.exe
8153bbd8     4     32     0     0  stdole32.tlb
8172f950   488    392     0     0  OBJECTS.DATA
8173e9c0     4      0     0     0  $Directory
814f4538     4      0     0     0  $Directory
81650790   344     48     0     0  INDEX.BTR
814f55f8     4      0     0     0  $Directory
...
814caef8     4      0     0     0  $Directory
8171cd90  1392     36     0     0  system
815f07f0     4      0     0     0  $Directory
814a2298     4      0     0     0  $Directory
81541538     4      0     0     0  $Directory
81585288    28      0     0     0  $Directory
8173f708     4      0     0     0  $Directory
...
8158cf10     4      0     0     0  $Directory
```

 

 





