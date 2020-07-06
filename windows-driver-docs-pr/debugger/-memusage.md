---
title: memusage
description: Memusage 扩展显示有关物理内存使用情况的摘要统计信息。
ms.assetid: 32796ada-53ee-465f-b284-db6ee5481878
keywords:
- memusage Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- memusage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 43000e448c5f7a400eeaccfa73a8a6b832276a4f
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968302"
---
# <a name="memusage"></a>!memusage


**！ Memusage**扩展显示有关物理内存使用情况的摘要统计信息。

语法

```dbgcmd
!memusage [Flags]
```

## <a name="span-idddk__memusage_dbgspanspan-idddk__memusage_dbgspanparameters"></a><span id="ddk__memusage_dbg"></span><span id="DDK__MEMUSAGE_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可以是下列值之一。 默认值为0x0。

<span id="0x0"></span><span id="0X0"></span>0x0  
显示一般摘要信息以及对 PFN 数据库中页面的更详细说明。 有关此类输出的示例，请参阅 "备注" 部分。

<span id="0x1"></span><span id="0X1"></span>0x1  
只显示有关 PFN 数据库中修改的非写入页的摘要信息。

<span id="0x2"></span><span id="0X2"></span>0x2  
仅显示有关 PFN 数据库中修改的非写入页的详细信息。

<span id="0x8"></span><span id="0X8"></span>0x8  
只显示有关内存使用情况的一般摘要信息。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

**模式**：仅限内核模式


 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

物理内存统计信息是从内存管理器的页面框架编号（PFN）数据库表中收集的。

此命令需要较长时间才能运行，特别是当目标计算机在64位模式下运行时，由于要获取的数据量更大，因此更是如此。 在加载 PFN 数据库时，计数器将显示其进度。 若要加快此加载速度，请使用[**CTRL + A （切换波特率）**](ctrl-a--toggle-baud-rate-.md)键增加 COM 端口速度，或使用[**Cache （设置缓存大小）**](-cache--set-cache-size-.md)命令增加缓存大小（可能为大约 10 MB）。

执行[本地内核调试](performing-local-kernel-debugging.md)时，还可以使用 **！ memusage**命令。

下面是此扩展的输出示例：

```dbgcmd
kd> !memusage
 loading PFN database
loading (98% complete)

Compiling memory usage data (100% Complete).
             Zeroed:     49 (   196 kb)
               Free:      5 (    20 kb)
            Standby:   5489 ( 21956 kb)
           Modified:    714 (  2856 kb)
    ModifiedNoWrite:      1 (     4 kb)
       Active/Valid:  10119 ( 40476 kb)
         Transition:      6 (    24 kb)
            Unknown:      0 (     0 kb)
              TOTAL:  16383 ( 65532 kb)

  Building kernel map
  Finished building kernel map
Scanning PFN database - (99% complete) 

  Usage Summary (in Kb):


Control Valid Standby Dirty Shared Locked PageTables  name

8251a258    12    108     0     0     0     0  mapped_file( cscui.dll )
827ab1b8     8   1708     0     0     0     0  mapped_file( $Mft )
8263c408   908     48     0     0     0     0  mapped_file( win32k.sys )
8252dda8     0    324     0     0     0     0  mapped_file( ShellIconCache )
8272f638   128    112     0   116     0     0  mapped_file( advapi32.dll )
......
82755958     0      4     0     0     0     0  mapped_file( $Directory )
8250b518     0      4     0     0     0     0    No Name for File
8254d8d8     0      4     0     0     0     0  mapped_file( $Directory )
82537be8     0      4     0     0     0     0  mapped_file( Windows Explorer.lnk )

--------  1348      0     0 ----- -----   904  process ( System )
--------   492      0     0 ----- -----    72  process ( winmine.exe )
--------  3364   1384  1396 ----- -----   188  process ( explorer.exe )
--------   972      0     0 ----- -----    88  process ( services.exe )
--------   496   1456   384 ----- -----   164  process ( winmgmt.exe )
--------  1144      0     0 ----- -----   120  process ( svchost.exe )
--------   944      0     0 ----- -----   156  process ( winlogon.exe )
--------   412      0     0 ----- -----    64  process ( csrss.exe )
......
--------    12      0     0 ----- -----     8  process ( wmiadap.exe )

--------   316      0     0 ----- -----     0  pagefile section (346e)
--------  4096      0     0 ----- -----     0  pagefile section (9ad)

--------   884    280    36 -----     0 -----  driver ( ntoskrnl.exe )
--------    88      8     0 -----     0 -----  driver ( hal.dll )
--------     8      0     0 -----     0 -----  driver ( kdcom.dll )
--------    12      0     0 -----     0 -----  driver ( BOOTVID.dll )
......
--------     8      0     0 -----     0 -----  driver ( ndisuio.sys )
--------    16      0     0 -----     0 -----  driver ( dump_scsiport.sys )
--------    56      0     0 -----     0 -----  driver ( dump_aic78xx.sys )
--------  2756   1060   876 -----     0 -----  driver ( Paged Pool )
--------  1936    128   148 -----     0 -----  driver ( Kernel Stacks )
--------     0      0     0 -----     0 -----  driver ( NonPaged Pool )
```

第一列显示描述每个映射结构的控件区域结构的地址。 使用[**！ ca**](-ca.md) extension 命令显示这些控件区域。

<a name="remarks"></a>备注
-------

可以使用[**！ vm**](-vm.md)扩展命令分析虚拟内存使用情况。 此扩展通常比 **！ memusage**更有用。 有关内存管理的详细信息，请参阅 Russinovich 和 David 所罗门群岛的*Microsoft Windows 内部机制*。 

[**！ Pfn**](-pfn.md) extension 命令可用于显示 pfn 数据库中的特定页面帧条目。

 

 





