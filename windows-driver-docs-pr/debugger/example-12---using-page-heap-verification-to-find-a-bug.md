---
title: 12 的示例使用页面堆验证，以查找 Bug
description: 12 的示例使用页面堆验证，以查找 Bug
ms.assetid: aa3f5c53-8522-48be-a3cd-49b740803fe3
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: a541f8ef5e454d73afebb0fd1ee48b251f453068
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521566"
---
# <a name="example-12-using-page-heap-verification-to-find-a-bug"></a>示例 12:使用页面堆验证来查找 Bug


## <span id="ddk_example_12___using_page_heap_verification_to_find_a_bug_dtools"></span><span id="DDK_EXAMPLE_12___USING_PAGE_HEAP_VERIFICATION_TO_FIND_A_BUG_DTOOLS"></span>


以下一系列命令演示了如何使用页面堆验证功能 GFlags 和 NTSD 调试器的堆内存使用中检测到错误。 在此示例中，程序员怀疑虚构的应用程序、 pheap buggy.exe，有一个堆错误，并通过一系列测试，以确定错误继续执行。

NTSD 的详细信息，请参阅[调试使用 CDB 和 NTSD](debugging-using-cdb-and-ntsd.md)。

### <a name="span-idstep1enablestandardpageheapverificationspanspan-idstep1enablestandardpageheapverificationspanspan-idstep1enablestandardpageheapverificationspanstep-1-enable-standard-page-heap-verification"></a><span id="Step_1__Enable_standard_page_heap_verification"></span><span id="step_1__enable_standard_page_heap_verification"></span><span id="STEP_1__ENABLE_STANDARD_PAGE_HEAP_VERIFICATION"></span>步骤 1:启用标准页面堆验证

以下命令启用 pheap 的标准页面堆验证-buggy.exe:

```console
gflags /p /enable pheap-buggy.exe
```

### <a name="span-idstep2verifythatpageheapisenabledspanspan-idstep2verifythatpageheapisenabledspanspan-idstep2verifythatpageheapisenabledspanstep-2-verify-that-page-heap-is-enabled"></a><span id="Step_2__Verify_that_page_heap_is_enabled"></span><span id="step_2__verify_that_page_heap_is_enabled"></span><span id="STEP_2__VERIFY_THAT_PAGE_HEAP_IS_ENABLED"></span>步骤 2:验证已启用该页面堆

以下命令将列出为其启用页堆验证图像文件：

```console
gflags /p
```

在响应中，GFlags 显示下面的程序列表。 在此显示中，**跟踪**指示标准页面堆验证，并**完整跟踪**指示整页堆验证。 在这种情况下，pheap buggy.exe 列出**跟踪**，指示标准页面堆验证是否启用了，按预期方式。

```console
pheap-buggy.exe: page heap enabled with flags (traces )
```

### <a name="span-idstep3runthedebuggerspanspan-idstep3runthedebuggerspanspan-idstep3runthedebuggerspanstep-3-run-the-debugger"></a><span id="Step_3__Run_the_debugger"></span><span id="step_3__run_the_debugger"></span><span id="STEP_3__RUN_THE_DEBUGGER"></span>步骤 3:运行调试器

以下命令将运行**CorruptAfterEnd**函数中与 NTSD 的 pheap buggy.exe **-g** （忽略初始断点） 和 **-x** （在上设置第二次中断访问冲突异常） 参数：

```console
ntsd -g -x pheap-buggy CorruptAfterEnd
```

NTSD 当应用程序失败时，生成以下显示，指示，它检测到错误 pheap-buggy.exe:

```dbgcmd
===========================================================
VERIFIER STOP 00000008: pid 0xAA0: corrupted suffix pattern

        00C81000 : Heap handle 
        00D81EB0 : Heap block 
        00000100 : Block size 
#         00000000 :
===========================================================

Break instruction exception - code 80000003 (first chance)
eax=00000000 ebx=00d81eb0 ecx=77f7e257 edx=0006fa18 esi=00000008 edi=00c81000
eip=77f7e098 esp=0006fc48 ebp=0006fc5c iopl=0         nv up ei pl zr na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=0038  gs=0000             efl=00000246
ntdll!DbgBreakPoint:
77f7e098 cc               int     3
```

标头信息包括具有已损坏的块的堆的地址 (00 C 81000:堆句柄），已损坏的块的地址 (00D81EB0:堆块） 和分配的大小 (00000100:块大小）。

"已损坏的后缀模式"消息指示应用程序违反 GFlags pheap buggy.exe 堆分配结束后插入的数据完整性模式。

### <a name="span-idstep4displaythecallstackspanspan-idstep4displaythecallstackspanspan-idstep4displaythecallstackspanstep-4-display-the-call-stack"></a><span id="Step_4__Display_the_call_stack"></span><span id="step_4__display_the_call_stack"></span><span id="STEP_4__DISPLAY_THE_CALL_STACK"></span>步骤 4:显示调用堆栈

在下一步中，使用 NTSD 报告，以找到导致此错误的函数的地址。 接下来两个命令启用转储的调试器和显示行号的调用堆栈中的行号。

```dbgcmd
C:\>.lines

Line number information will be loaded 

C:\>kb

ChildEBP RetAddr  Args to Child
WARNING: Stack unwind information not available. Following frames may be wrong.
0006fc5c 77f9e6dd 00000008 77f9e3e8 00c81000 ntdll!DbgBreakPoint
0006fcd8 77f9f3c8 00c81000 00000004 00d81eb0 ntdll!RtlpNtEnumerateSubKey+0x2879
0006fcfc 77f9f5bb 00c81000 01001002 00000010 ntdll!RtlpNtEnumerateSubKey+0x3564
0006fd4c 77fa261e 00c80000 01001002 00d81eb0 ntdll!RtlpNtEnumerateSubKey+0x3757
0006fdc0 77fc0dc2 00c80000 01001002 00d81eb0 ntdll!RtlpNtEnumerateSubKey+0x67ba
0006fe78 77fbd87b 00c80000 01001002 00d81eb0 ntdll!RtlSizeHeap+0x16a8
0006ff24 010013a4 00c80000 01001002 00d81eb0 ntdll!RtlFreeHeap+0x69
0006ff3c 01001450 00000000 00000001 0006ffc0 pheap-buggy!TestCorruptAfterEnd+0x2b [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 185]
0006ff4c 0100157f 00000002 00c65a68 00c631d8 pheap-buggy!main+0xa9 [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 69]
0006ffc0 77de43fe 00000000 00000001 7ffdf000 pheap-buggy!mainCRTStartup+0xe3 [crtexe.c @ 349]
0006fff0 00000000 0100149c 00000000 78746341 kernel32!DosPathToSessionPathA+0x204
```

因此，调试器将具有行号显示 pheap buggy.exe 的调用堆栈。 调用堆栈显示显示的错误时出错**TestCorruptAfterEnd** pheap buggy.exe 中的函数尝试通过调用释放的分配在 0x00c80000 **HeapFree**，重定向到**RtlFreeHeap**。

此错误最可能原因是缓冲区的该程序编写了它在此函数中分配的末尾。

### <a name="span-idstep5enablefullpageheapverificationspanspan-idstep5enablefullpageheapverificationspanspan-idstep5enablefullpageheapverificationspanstep-5-enable-full-page-heap-verification"></a><span id="Step_5__Enable_full_page_heap_verification"></span><span id="step_5__enable_full_page_heap_verification"></span><span id="STEP_5__ENABLE_FULL_PAGE_HEAP_VERIFICATION"></span>步骤 5:启用整页堆验证

与不同的标准页面堆验证整页堆验证可以捕获此堆缓冲区的滥用，一旦它发生。 以下命令启用 pheap 整页堆验证-buggy.exe:

```console
gflags /p /enable pheap-buggy.exe /full
```

### <a name="span-idstep6verifythatfullpageheapisenabledspanspan-idstep6verifythatfullpageheapisenabledspanspan-idstep6verifythatfullpageheapisenabledspanstep-6-verify-that-full-page-heap-is-enabled"></a><span id="Step_6__Verify_that_full_page_heap_is_enabled"></span><span id="step_6__verify_that_full_page_heap_is_enabled"></span><span id="STEP_6__VERIFY_THAT_FULL_PAGE_HEAP_IS_ENABLED"></span>步骤 6:验证已启用该整页堆

以下命令列出了为其启用页堆验证程序：

```console
gflags /p
```

在响应中，GFlags 显示下面的程序列表。 在此显示中，**跟踪**指示标准页面堆验证，并**完整跟踪**指示整页堆验证。 在这种情况下，pheap buggy.exe 列出**完整的跟踪**，指示启用了整页堆验证，按预期方式。

```console
pheap-buggy.exe: page heap enabled with flags (full traces )
```

### <a name="span-idstep7runthedebuggeragainspanspan-idstep7runthedebuggeragainspanspan-idstep7runthedebuggeragainspanstep-7-run-the-debugger-again"></a><span id="Step_7__Run_the_debugger_again"></span><span id="step_7__run_the_debugger_again"></span><span id="STEP_7__RUN_THE_DEBUGGER_AGAIN"></span>步骤 7:再次运行调试器

以下命令将运行**CorruptAfterEnd**函数中使用的是 NTSD 调试器的 pheap buggy.exe **-g** （忽略初始断点） 和 **-x** （设置第二次访问冲突异常时中断) 参数：

```console
ntsd -g -x pheap-buggy CorruptAfterEnd
```

NTSD 当应用程序失败时，生成以下显示，指示，它检测到错误 pheap-buggy.exe:

```console
Page heap: process 0x5BC created heap @ 00880000 (00980000, flags 0x3)
ModLoad: 77db0000 77e8c000   kernel32.dll
ModLoad: 78000000 78046000   MSVCRT.dll
Page heap: process 0x5BC created heap @ 00B60000 (00C60000, flags 0x3)
Page heap: process 0x5BC created heap @ 00C80000 (00D80000, flags 0x3)
Access violation - code c0000005 (first chance)
Access violation - code c0000005 (!!! second chance !!!)
eax=00c86f00 ebx=00000000 ecx=77fbd80f edx=00c85000 esi=00c80000 edi=00c16fd0
eip=01001398 esp=0006ff2c ebp=0006ff4c iopl=0         nv up ei pl nz na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=0038  gs=0000             efl=00000206
pheap-buggy!TestCorruptAfterEnd+1f:
01001398 889801010000     mov     [eax+0x101],bl          ds:0023:00c87001=??
```

使用启用了整页堆验证，调试器将中断处访问冲突。 若要查找访问冲突的精确位置，打开行号转储并显示调用堆栈跟踪。

带编号的调用堆栈跟踪显示，如下所示：显示问题的行以粗体文本显示。

```console
ChildEBP RetAddr  Args to Child
0006ff3c 01001450 00000000 00000001 0006ffc0 pheap-buggy!TestCorruptAfterEnd+0x1f [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 184]
0006ff4c 0100157f 00000002 00c16fd0 00b70eb0 pheap-buggy!main+0xa9 [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 69]
0006ffc0 77de43fe 00000000 00000001 7ffdf000 pheap-buggy!mainCRTStartup+0xe3 [crtexe.c @ 349]
WARNING: Stack unwind information not available. Following frames may be wrong.
0006fff0 00000000 0100149c 00000000 78746341 kernel32!DosPathToSessionPathA+0x204
```

堆栈跟踪显示 pheap buggy.exe 184 行中出现问题。 由于启用了整页堆验证，调用堆栈开始在程序代码中，不在系统 DLL。 因此，发生，而不是堆块已释放时捕获冲突。

### <a name="span-idstep8locatetheerrorinthecodespanspan-idstep8locatetheerrorinthecodespanspan-idstep8locatetheerrorinthecodespanstep-8-locate-the-error-in-the-code"></a><span id="Step_8__Locate_the_error_in_the_code"></span><span id="step_8__locate_the_error_in_the_code"></span><span id="STEP_8__LOCATE_THE_ERROR_IN_THE_CODE"></span>步骤 8:在代码中查找错误

快速检查揭示问题的原因：该程序尝试写入的 257th 字节 (0x101) 的 256 字节 (0x100) 缓冲区，一种常见关闭--一个错误。

```console
*((PCHAR)Block + 0x100) = 0;
```

 

 





