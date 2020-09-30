---
title: DTrace 代码示例
description: 了解支持 D 编程语言的 DTrace。 请参阅代码示例并查看附加的可用支持。
ms.assetid: abf23d76-423d-4d1e-afde-83739015bbff
keywords:
- DTrace WDK
- 软件跟踪 WDK，DTrace
- 显示跟踪消息
- 格式化跟踪消息 WDK DTrace
- 跟踪消息格式 WDK DTrace
- 软件跟踪 WDK，设置消息格式
- 跟踪 WDK，DTrace
- 跟踪消息格式化文件 WDK
ms.date: 11/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: 42e85a1373e65bfe7a1a7ab6a143445fd1a2399a
ms.sourcegitcommit: f1d6c2d0cdbecdc69ba65ed3b530755fc73c8e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91590378"
---
# <a name="dtrace-code-samples"></a>DTrace 代码示例

DTrace 支持 D 编程语言。 本主题提供了 D 代码示例。

有关 Windows 上的 DTrace 的一般信息，请参阅 [dtrace](dtrace.md)。

有关 DTrace 的详细信息，请参阅剑桥大学的 [OpenDTrace 规范1.0 版](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-924.pdf) 。

> [!NOTE]
> 版本18980和 Windows Server 有问必答 Preview 版本18975后，Windows 内部版本支持 DTrace。

## <a name="additional-sample-scripts"></a>其他示例脚本

DTrace 源代码的示例目录中提供了适用于 Windows 方案的其他 D 脚本。

[https://github.com/microsoft/DTrace-on-Windows/tree/master/samples/windows](https://github.com/microsoft/DTrace-on-Windows/tree/master/samples/windows)

提供一组有用的 opentrace 工具包脚本 [https://github.com/opendtrace/toolkit](https://github.com/opendtrace/toolkit) 。


## <a name="disk-usage-by-name"></a>按名称的磁盘使用情况

此脚本提供给定可执行文件名称的磁盘计数器。 可执行文件的名称区分大小写，并且在脚本启动时在命令行上提供。

```dtrace

#pragma D option quiet
#pragma D option destructive


intptr_t curptr;
struct nt`_EPROCESS *eprocess_ptr;
int found;
int firstpass;
BEGIN
{
    curptr = (intptr_t) ((struct nt`_LIST_ENTRY *) (void*)&nt`PsActiveProcessHead)->Flink;  
    found = 0;
    firstpass = 1;
    bytesread = 0;
    byteswrite = 0;
    readcount = 0;
    writecount = 0;
    flushcount = 0;
}

tick-1ms

/found == 0/

{
/* use this for pointer parsing */
    if (found == 0)
    {
        eprocess_ptr = (struct nt`_EPROCESS *)(curptr - offsetof(nt`_EPROCESS, ActiveProcessLinks));
        processid = (string) eprocess_ptr->ImageFileName;

        if ($1 == processid)
        {
            found = 1;
        }

        else 
        {
            curptr = (intptr_t) ((struct nt`_LIST_ENTRY *) (void*)curptr)->Flink;
        }
    }       
}

tick-2s

{
    system ("cls");
    if (found == 1)
    {
        if (firstpass)
        {
            firstpass = 0;
            bytesread = (unsigned long long) eprocess_ptr->DiskCounters->BytesRead;
            byteswrite = (unsigned long long) eprocess_ptr->DiskCounters->BytesWritten;
            readcount = eprocess_ptr->DiskCounters->ReadOperationCount;
            writecount = eprocess_ptr->DiskCounters->WriteOperationCount;
            flushcount =  eprocess_ptr->DiskCounters->FlushOperationCount;
        }

        else
        {
            bytesread = (unsigned long long)  (eprocess_ptr->DiskCounters->BytesRead - bytesread);
            byteswrite = (unsigned long long)  (eprocess_ptr->DiskCounters->BytesWritten - byteswrite);
            readcount = eprocess_ptr->DiskCounters->ReadOperationCount - readcount;
            writecount = eprocess_ptr->DiskCounters->WriteOperationCount - writecount;      
            flushcount = eprocess_ptr->DiskCounters->FlushOperationCount - flushcount;

            printf("*** Reports disk read/write every second *** \n");
            printf("Process name: %s\n", eprocess_ptr->ImageFileName);
            printf("Process Id: %d\n", (int) eprocess_ptr->UniqueProcessId);
            printf("Bytes Read %llu \n",  (unsigned long long) bytesread);
            printf("Bytes Written %llu \n", (unsigned long long) byteswrite);
            printf("Read Operation Count %d \n", readcount);
            printf("Write Operation Count %d \n",writecount);
            printf("Flush Operation Count %d \n", flushcount);

            bytesread = (unsigned long long) eprocess_ptr->DiskCounters->BytesRead;
            byteswrite = (unsigned long long) eprocess_ptr->DiskCounters->BytesWritten;
            readcount = eprocess_ptr->DiskCounters->ReadOperationCount;
            writecount = eprocess_ptr->DiskCounters->WriteOperationCount;
            flushcount =  eprocess_ptr->DiskCounters->FlushOperationCount;      
        }       
    }

    else
    {
        printf("No matching process found for %s \n", $1);
        exit(0);
    }
}
```

将该文件另存为 diskuagebyname，并使用-s 选项运行测试脚本。 为所需的 exe 提供区分大小写的名称（例如 Notepad.exe

```dtrace

C:\>dtrace -s diskusagebyname.d Notepad.exe

*** Reports disk read/write every second *** 
Process name: Notepad.exe
Process Id: 6012
Bytes Read 0 
Bytes Written 0 
Read Operation Count 0 
Write Operation Count 0 
Flush Operation Count 0 
*** Reports disk read/write every second *** 
Process name: cmd.exe
Process Id: 4428
Bytes Read 18446744073709480960 
Bytes Written 18446744073709522944 
Read Operation Count -5 
Write Operation Count -7 
Flush Operation Count 0 

```

若要保留正在运行的磁盘日志活动，请将命令重定向到文本文件，如下所示。

```dtrace
C:\>dtrace -s diskusagebyname.d Notepad.exe>>diskstats.txt
```

## <a name="dumping-memory-usage"></a>转储内存使用量

在某些诊断情况下，需要转储内核结构来了解这种情况。 此代码显示了转储系统内存使用量的示例。 下面的 D 脚本每3秒激发一次计时器探测并刷新系统内存使用量。

```dtrace
#pragma D option quiet
#pragma D option destructive

tick-3s
{
    system ("cls");

    this->pp = ((struct nt`_MI_PARTITION *) &nt`MiSystemPartition);

    printf("***** Printing System wide page information ******* \n");
    printf( "Total Pages Entire Node: %u MB \n", this->pp->Core.NodeInformation->TotalPagesEntireNode*4096/(1024*1024));
    printf("Total Available Pages: %u Mb \n", this->pp->Vp.AvailablePages*4096/(1024*1024));
    printf("Total ResAvail Pages: %u  Mb \n",  this->pp->Vp.ResidentAvailablePages*4096/(1024*1024));
    printf("Total Shared Commit: %u  Mb \n",  this->pp->Vp.SharedCommit*4096/(1024*1024));
    printf("Total Pages for PagingFile: %u  Mb \n",  this->pp->Vp.TotalPagesForPagingFile*4096/(1024*1024));
    printf("Modified Pages : %u  Mb \n",  this->pp->Vp.ModifiedPageListHead.Total*4096/(1024*1024));
    printf("Modified No Write Page Count : %u  Mb \n",  this->pp->Vp.ModifiedNoWritePageListHead.Total*4096/(1024*1024));
    printf("Bad Page Count : %d  Mb \n",  this->pp->PageLists.BadPageListHead.Total*4096/(1024*1024));
    printf("Zero Page Count : %d  Mb \n",  this->pp->PageLists.ZeroedPageListHead.Total*4096/(1024*1024));
    printf("Free Page Count : %d  Mb \n",  this->pp->PageLists.FreePageListHead.Total*4096/(1024*1024));


/********** Printing Commit info ******************/ 
    
    this->commit = ((struct nt`_MI_PARTITION_COMMIT ) ((struct nt`_MI_PARTITION *) &nt`MiSystemPartition)->Commit);

    printf("***** Printing Commit Info ******* \n");
    printf("Total Committed Pages: %u  Mb \n", this->pp->Vp.TotalCommittedPages*4096/(1024*1024));
    printf("Total Commit limit: %u  Mb  \n", this->pp->Vp.TotalCommitLimit*4096/(1024*1024));
    printf("Peak Commitment: %u Mb \n", this->commit.PeakCommitment*4096/(1024*1024));
    printf("Low Commit Threshold: %u Mb \n", this->commit.LowCommitThreshold*4096/(1024*1024));
    printf("High Commit Threshold: %u Mb \n", this->commit.HighCommitThreshold*4096/(1024*1024));
    printf("System Commit Reserve: %u Mb \n", this->commit.SystemCommitReserve*4096/(1024*1024));
    

}
```

将该文件另存为 dumpmemoryusage。

此示例使用符号，因此如安装中所述设置符号路径。

```cmd
set _NT_SYMBOL_PATH=srv*C:\symbols*https://msdl.microsoft.com/download/symbols 
```
使用-s 选项运行测试脚本。

```dtrace
C:\>dtrace -s dumpmemoryusage.d
***** Printing System wide page information ******* 
Total Pages Entire Node: 2823 MB 
Total Available Pages: 622 Mb 
Total ResAvail Pages: 2369  Mb 
Total Shared Commit: 166  Mb 
Total Pages for PagingFile: 30  Mb 
Modified Pages : 30  Mb 
Modified No Write Page Count : 0  Mb 
Bad Page Count : 0  Mb 
Zero Page Count : 7  Mb 
Free Page Count : 0  Mb 
***** Printing Commit Info ******* 
Total Committed Pages: 2401  Mb 
Total Commit limit: 4551  Mb  
Peak Commitment: 2989 Mb 
Low Commit Threshold: 3413 Mb 
High Commit Threshold: 4295 Mb 
System Commit Reserve: 5 Mb 
```

此程序旨在继续监视内存使用情况。 按 CTRL + C 退出。

## <a name="identifying-heap-free-time-breakdown-for-an-activity"></a>标识活动的堆空闲时间细分

此示例提供了  [RtlFreeHeap](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlfreeheap) 函数到子函数的细分，并显示了执行这些函数所用的最长时间。

```dtrace
/* Mark script destructive as we call "cls" in the tick-1sec provider*/
#pragma D option destructive

/* Program to calculate time taken in RtlFreeHeap function. Hit Ctrl-C to break. */ 

dtrace:::BEGIN 
{
    counter1 = 0;

}

tick-1sec
{
    system ("cls");
    printf("count of function hit = %d << Press Ctrl-C to exit >> \n", counter1);

}

/* Instrument entry of RtlFreeHeap*/

pid$1:ntdll:RtlFreeHeap:entry
{ 
    /* self is thread local */
    self->ts = timestamp;
    self->depth = 0;
    counter1++;
} 

pid$1:ntdll:RtlFreeHeap:return
/self->ts/
{
    this->ts = timestamp - self->ts;
    @disttime = quantize(this->ts); 
    @funcName[probemod,probefunc] = max(this->ts);  
    self->ts = 0;
}


pid$1:::entry
/ self->ts /
{
    self->functime[self->depth] = timestamp;
    self->depth++;
}

pid$1:::return
/ self->ts /
{
    if (self->depth > 0)
    {
        self->depth--;
        /* this is a local scope */
        this->ts = timestamp - self->functime[self->depth];
        @funcName[probemod,probefunc] = max(this->ts);
    }
}

END

{
    system ("cls");
    /* Print overall time distribution for RtlFreeHeap */
    printa (@disttime);
    /* Print top 15 functions along with average time spent executing them */
    trunc (@funcName, 15);
    
    printa( @funcName);
    
}

```

将该文件另存为 heapfree。

此脚本采用进程 ID 或 PID。 若要测试脚本，请在命令提示符下运行 tasklist，并找到所需的 PID。

```dtrace
C:\>tasklist

Image Name                     PID Session Name        Session#    Mem Usage
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0          8 K
System                           4 Services                   0        108 K
Registry                        72 Services                   0     35,576 K

...

Notepad.exe                   7944 31C5CE94259D4006           2     20,736 K

```

指定 PID 作为参数，并使用-s 选项运行测试脚本，如下所示。

```dtrace
C:\>dtrace -s heapfree.d 7944

count of function hit = 28 <<Press Ctrl-C to exit>>
```

在与 PID 关联的程序中执行所需的任务，例如，在记事本中键入或更改字体。

按 CRTL，堆使用情况将与堆栈信息一起显示。

```dtrace
           value  ------------- Distribution ------------- count
            4096 |                                         0
            8192 |@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@        23
           16384 |@@@@@@                                   4
           32768 |                                         0
           65536 |                                         0
          131072 |@                                        1
          262144 |                                         0


  ntdll                                               RtlTryEnterCriticalSection                                     9444
  ntdll                                               RtlGetCurrentServiceSessionId                                 12302
  ntdll                                               RtlFreeHeap                                                  151354
  ```

## <a name="memory-pool-tracking"></a>内存池跟踪

注意：请以 aggsortkeypos 变量集运行此脚本。 此变量通知 D 跟踪根据第一个索引 (大小) 来对输出进行排序。

用法：

`dtrace -s <script.d>  <Time> <Tag> -x  aggsortkey -x aggsortkeypos=1` 

跟踪 KSec 泄漏的示例： dtrace-s PoolTrackingSummary "120s" 0x6365734b-x aggsortkey-x aggsortkeypos = 1 

`<Tag>`该值是内存池标记的已编码 ASCII 值。 例如，若要对 nt 文件系统 NtFf 的标记值进行编码，请首先反转两组字母，这会是 fFtN。 将 ASCII 字符转换为十六进制将是 46 66 74 4e 或0x4666744e 作为我们的程序的参数。

另一个示例是转换 Ksec。

首先反转字母的顺序： cesK

然后将这些字符转换为十六进制、63 65 73 4b 或0x6365734b 作为程序的参数。

请注意，大小写小写对于与池标记匹配非常重要。

输出：脚本运行120秒，并输出 KSec 分配/免费摘要。 可以将此设置为任何需要的时间。

```dtrace
#pragma D option destructive
#pragma D option quiet
#pragma D option dynvarsize=240m 
#pragma D option bufsize=120m
#pragma D option aggsize=120m 


fbt:nt:ExAllocatePoolWithTag:entry
{   
    /* This is E100 in reserve. Convert ASCII to Hex => Hex('001E').*/
    if (arg2 == $2) 
    { 
        self->size = (unsigned int) arg1;
        @allocstack[stack(), self->size] = count();
    }
}

fbt:nt:ExAllocatePoolWithTag:return
/self->size/
{
    @mem[(uintptr_t) arg1] = sum(1);
    addr[(uintptr_t) arg1] = 1;
    /* printf("%Y: Execname %s allocated size %d bytes return ptr %x", walltimestamp, execname, (uint64_t) self->size, (uintptr_t) arg1 );*/

    size[(uintptr_t) arg1] = self->size;
    @sizealloc[self->size] = count();
    @delta[self->size] = sum(1);
    
    self->size = 0;
}

fbt:nt:ExFreePoolWithTag:entry
/addr[(uintptr_t) arg0]/
{
    @mem[(uintptr_t) arg0] = sum (-1);
    addr[(uintptr_t) arg0] -= 1;

    @sizefree[size[(uintptr_t) arg0]] = count();
    @delta[size[(uintptr_t) arg0]] = sum(-1);
}

tick-$1
{   
    exit(0);
}

END 
{

   printf("%10s %10s %10s %10s\n", "SIZE", "ALLOC", "FREE", "DELTA");
   printa("%10d %@10d %@10d %@10d\n", @sizealloc, @sizefree, @delta);

   printf("Printing stacks \n");
   printa (@allocstack);
    
   printf("== REPORT ==\n\n");
   printa("0x%x => %@u\n",@mem);
}

```

将该文件另存为 pooltrackingsummary，并使用-s 选项运行测试脚本，并提供前面讨论的标记值和其他参数。

120s 选项时，程序运行了两分钟。 在此期间，请使用 Windows 来执行监视的内存池。 例如，加载并卸载 web 浏览器或其他程序。

```dtrace
C:\>dtrace -s pooltrackingsummary.d "120s" 0x4666744e -x aggsortkey -x aggsortkeypos=1
      SIZE      ALLOC       FREE      DELTA
      1552         16          0         16
Printing stacks

              Ntfs.sys`NtfsCreateFcb+0x388
              Ntfs.sys`NtfsCreateNewFile+0xaa8
              Ntfs.sys`NtfsCommonCreate+0x2303
              Ntfs.sys`NtfsFsdCreate+0x284
              nt`IofCallDriver+0x55
              FLTMGR.SYS`FltpLegacyProcessingAfterPreCallbacksCompleted+0x1b9
              FLTMGR.SYS`FltpCreate+0x324
              nt`IofCallDriver+0x55
              nt`IoCallDriverWithTracing+0x34
              nt`IopParseDevice+0x6ac
              nt`ObpLookupObjectName+0x3fe
              nt`ObOpenObjectByNameEx+0x1fa
              nt`IopCreateFile+0x40f
              nt`NtCreateFile+0x79
              nt`KiSystemServiceCopyEnd+0x38
     1552                3

              Ntfs.sys`NtfsCreateFcb+0x388
              Ntfs.sys`NtfsOpenFile+0x2d7
              Ntfs.sys`NtfsCommonCreate+0x25a8
              Ntfs.sys`NtfsFsdCreate+0x284
              nt`IofCallDriver+0x55
              FLTMGR.SYS`FltpLegacyProcessingAfterPreCallbacksCompleted+0x1b9
              FLTMGR.SYS`FltpCreate+0x324
              nt`IofCallDriver+0x55
              nt`IoCallDriverWithTracing+0x34
              nt`IopParseDevice+0x6ac
              nt`ObpLookupObjectName+0x3fe
              nt`ObOpenObjectByNameEx+0x1fa
              nt`IopCreateFile+0x40f
              nt`NtCreateFile+0x79
              nt`KiSystemServiceCopyEnd+0x38
     1552                4

              Ntfs.sys`NtfsCreateFcb+0x388
              Ntfs.sys`NtfsOpenFile+0x2d7
              Ntfs.sys`NtfsCommonCreate+0x25a8
              Ntfs.sys`NtfsFsdCreate+0x284
              nt`IofCallDriver+0x55
              FLTMGR.SYS`FltpLegacyProcessingAfterPreCallbacksCompleted+0x1b9
              FLTMGR.SYS`FltpCreate+0x324
              nt`IofCallDriver+0x55
              nt`IoCallDriverWithTracing+0x34
              nt`IopParseDevice+0x6ac
              nt`ObpLookupObjectName+0x3fe
              nt`ObOpenObjectByNameEx+0x1fa
              nt`IopCreateFile+0x40f
              nt`NtOpenFile+0x58
              nt`KiSystemServiceCopyEnd+0x38
     1552                3

...

== REPORT ==

0xffffd304c98dd380 => 1
0xffffd304cc4655a0 => 1
0xffffd304cccf15a0 => 1
0xffffd304ccdeb990 => 1
0xffffd304ce048760 => 1
0xffffd304cf1ee990 => 1
0xffffd304d0473010 => 1
0xffffd304d12075a0 => 1
0xffffd304d14135a0 => 1
0xffffd304d1674010 => 1
0xffffd304d33b3660 => 1
0xffffd304d3b29010 => 1
0xffffd304d42c6010 => 1
0xffffd304d48b2010 => 1
0xffffd304de1fa5f0 => 1
0xffffd304e1ad56a0 => 1
```

## <a name="comparing-guids"></a>比较 Guid

虽然 DTrace 不支持本机 GUID，但您可以在此示例代码中创建结构来处理它们。 下面是如何比较 Guid 的示例。

```dtrace
nt`_GUID guidcmp;


/* Sleep After GUID: 29f6c1db-86da-48c5-9fdb-f2b67b1f44da */
dtrace:::BEGIN
{
    printf("Begin\n");
    guidcmp.Data1 = 0x29f6c1db;
    guidcmp.Data2 = 0x86da;
    guidcmp.Data3 = 0x48c5;
    guidcmp.Data4[0] = 0x9f;
    guidcmp.Data4[1]  = 0xdb;
    guidcmp.Data4[2]  = 0xf2;
    guidcmp.Data4[3]  = 0xb6;
    guidcmp.Data4[4]  = 0x7b;
    guidcmp.Data4[5]  = 0x1f;
    guidcmp.Data4[6]  = 0x44;
    guidcmp.Data4[7]  = 0xda;
}

pid$target:PowrProf:PowerReadACValueIndexEx:entry 
{ 
    cidstr = (nt`_GUID *) (copyin(arg2, sizeof(nt`_GUID))); 

    printf("\nPrinting GUID to compare\n");
    print(guidcmp);

    printf("\nPrinting GUID received \n");
    print(*cidstr);

    if (    (cidstr->Data1 == guidcmp.Data1) &&
        (cidstr->Data2 == guidcmp.Data2) &&
        (cidstr->Data3 == guidcmp.Data3) &&
        (cidstr->Data4[0] == guidcmp.Data4[0]) &&
        (cidstr->Data4[1] == guidcmp.Data4[1]) &&
        (cidstr->Data4[2] == guidcmp.Data4[2]) &&
        (cidstr->Data4[3] == guidcmp.Data4[3]) &&
        (cidstr->Data4[4] == guidcmp.Data4[4]) &&
        (cidstr->Data4[5] == guidcmp.Data4[5]) &&
        (cidstr->Data4[6] == guidcmp.Data4[6]) &&
        (cidstr->Data4[7] == guidcmp.Data4[7])  )
    {
        printf("GUID matched \n");
    }
    else
    {
        printf("No match");
    }
}

dtrace:::END
{
    printf("End\n");
}
```

将该文件另存为 comparequid，并使用-s 选项运行测试脚本，提供如下所示的参数。

```dtrace
C:\Windows\system32>dtrace -s compareguid.d -c "powercfg /qh scheme_current sub_sleep standbyidle"
dtrace: script 'compareguid.d' matched 9 probes
CPU     ID                    FUNCTION:NAME
  0      1                           :BEGIN Begin
 
Power Scheme GUID: 381b4222-f694-41f0-9685-ff5bb260df2e  (Balanced)
  GUID Alias: SCHEME_BALANCED
  Subgroup GUID: 238c9fa8-0aad-41ed-83f4-97be242c8f20  (Sleep)
    GUID Alias: SUB_SLEEP
    Power Setting GUID: 29f6c1db-86da-48c5-9fdb-f2b67b1f44da  (Sleep after)
      GUID Alias: STANDBYIDLE
      Minimum Possible Setting: 0x00000000
      Maximum Possible Setting: 0xffffffff
      Possible Settings increment: 0x00000001
      Possible Settings units: Seconds
    Current AC Power Setting Index: 0x00000708
   Current DC Power Setting Index: 0x00000384
 
dtrace: pid 7560 has exited
  0  42695    PowerReadACValueIndexEx:entry
Printing GUID to compare
struct _GUID {
    UInt32 Data1 = 0x29f6c1db
    UInt16 Data2 = 0x86da
    UInt16 Data3 = 0x48c5
    UInt8 [8] Data4 = [ 0x9f, 0xdb, 0xf2, 0xb6, 0x7b, 0x1f, 0x44, 0xda ]
}
Printing GUID received
struct _GUID {
    UInt32 Data1 = 0x29f6c1db
    UInt16 Data2 = 0x86da
    UInt16 Data3 = 0x48c5
    UInt8 [8] Data4 = [ 0x9f, 0xdb, 0xf2, 0xb6, 0x7b, 0x1f, 0x44, 0xda ]
}
  0  42695    PowerReadACValueIndexEx:entry GUID matched
```

## <a name="see-also"></a>另请参阅

[Windows 上的 DTrace](dtrace.md)

[DTrace Windows 编程](dtrace-programming.md)

[DTrace ETW](dtrace-etw.md)

[DTrace 实时转储](dtrace-live-dump.md)