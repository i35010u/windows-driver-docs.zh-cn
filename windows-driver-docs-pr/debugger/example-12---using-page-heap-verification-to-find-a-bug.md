---
title: 示例12使用页堆验证查找 Bug
description: 示例12使用页堆验证查找 Bug
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4c76d89c0958fdb683ce47a61763f1292496950e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838821"
---
# <a name="example-12-using-page-heap-verification-to-find-a-bug"></a>示例12：使用页堆验证查找 Bug


## <span id="ddk_example_12___using_page_heap_verification_to_find_a_bug_dtools"></span><span id="DDK_EXAMPLE_12___USING_PAGE_HEAP_VERIFICATION_TO_FIND_A_BUG_DTOOLS"></span>


以下一系列命令演示了如何使用 GFlags 和 NTSD 调试器的页堆验证功能来检测堆内存使用中的错误。 在此示例中，程序员怀疑某个虚构应用程序 pheap-buggy.exe 有一个堆错误，并通过一系列测试来识别错误。

有关 NTSD 的详细信息，请参阅 [使用 CDB 和 NTSD 进行调试](debugging-using-cdb-and-ntsd.md)。

### <a name="span-idstep_1__enable_standard_page_heap_verificationspanspan-idstep_1__enable_standard_page_heap_verificationspanspan-idstep_1__enable_standard_page_heap_verificationspanstep-1-enable-standard-page-heap-verification"></a><span id="Step_1__Enable_standard_page_heap_verification"></span><span id="step_1__enable_standard_page_heap_verification"></span><span id="STEP_1__ENABLE_STANDARD_PAGE_HEAP_VERIFICATION"></span>步骤1：启用标准页堆验证

以下命令为 pheap-buggy.exe 启用标准页堆验证：

```console
gflags /p /enable pheap-buggy.exe
```

### <a name="span-idstep_2__verify_that_page_heap_is_enabledspanspan-idstep_2__verify_that_page_heap_is_enabledspanspan-idstep_2__verify_that_page_heap_is_enabledspanstep-2-verify-that-page-heap-is-enabled"></a><span id="Step_2__Verify_that_page_heap_is_enabled"></span><span id="step_2__verify_that_page_heap_is_enabled"></span><span id="STEP_2__VERIFY_THAT_PAGE_HEAP_IS_ENABLED"></span>步骤2：验证是否已启用页堆

以下命令将列出为其启用页堆验证的图像文件：

```console
gflags /p
```

在响应中，GFlags 显示以下程序列表。 在此显示中，" **跟踪** " 指示标准页堆验证，而 " **完全跟踪** " 指示完全页堆验证。 在这种情况下，pheap-buggy.exe 会与 **跟踪** 一起列出，这表示启用了标准页堆验证。

```console
pheap-buggy.exe: page heap enabled with flags (traces )
```

### <a name="span-idstep_3__run_the_debuggerspanspan-idstep_3__run_the_debuggerspanspan-idstep_3__run_the_debuggerspanstep-3-run-the-debugger"></a><span id="Step_3__Run_the_debugger"></span><span id="step_3__run_the_debugger"></span><span id="STEP_3__RUN_THE_DEBUGGER"></span>步骤3：运行调试器

以下命令使用 **-g** (忽略初始) 断点 pheap-buggy.exe 在 NTSD 中运行的 **CorruptAfterEnd** 函数 **， (对** 访问冲突异常设置第二次中断) 参数：

```console
ntsd -g -x pheap-buggy CorruptAfterEnd
```

当应用程序失败时，NTSD 会生成以下显示，这表示它在 pheap-buggy.exe 检测到错误：

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

标头信息包括具有损坏的块的堆的地址 (00C81000：堆句柄) ，损坏块 (00D81EB0：堆块) 的地址，以及分配 (00000100：块大小) 的大小。

"损坏的后缀模式" 消息指示应用程序违反了 GFlags 在 pheap-buggy.exe 堆分配末尾后插入的数据完整性模式。

### <a name="span-idstep_4__display_the_call_stackspanspan-idstep_4__display_the_call_stackspanspan-idstep_4__display_the_call_stackspanstep-4-display-the-call-stack"></a><span id="Step_4__Display_the_call_stack"></span><span id="step_4__display_the_call_stack"></span><span id="STEP_4__DISPLAY_THE_CALL_STACK"></span>步骤4：显示调用堆栈

在下一步中，使用 NTSD 报告的地址来查找导致错误的函数。 接下来的两个命令打开调试器中的行号转储，并显示带有行号的调用堆栈。

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

因此，调试器会显示带有行号 pheap-buggy.exe 的调用堆栈。 "调用堆栈" 显示显示错误在 pheap-buggy.exe 中的 **TestCorruptAfterEnd** 函数尝试通过调用 **HeapFree** 在0x00c80000 上释放分配时出错，并重定向到 **RtlFreeHeap**。

此错误的最可能原因是，程序在此函数中分配的缓冲区末尾结束。

### <a name="span-idstep_5__enable_full_page_heap_verificationspanspan-idstep_5__enable_full_page_heap_verificationspanspan-idstep_5__enable_full_page_heap_verificationspanstep-5-enable-full-page-heap-verification"></a><span id="Step_5__Enable_full_page_heap_verification"></span><span id="step_5__enable_full_page_heap_verification"></span><span id="STEP_5__ENABLE_FULL_PAGE_HEAP_VERIFICATION"></span>步骤5：启用整页堆验证

与标准页堆验证不同，整页堆验证一旦发生，就可以捕获此堆缓冲区的滥用。 以下命令启用对 pheap-buggy.exe 的完整页面堆验证：

```console
gflags /p /enable pheap-buggy.exe /full
```

### <a name="span-idstep_6__verify_that_full_page_heap_is_enabledspanspan-idstep_6__verify_that_full_page_heap_is_enabledspanspan-idstep_6__verify_that_full_page_heap_is_enabledspanstep-6-verify-that-full-page-heap-is-enabled"></a><span id="Step_6__Verify_that_full_page_heap_is_enabled"></span><span id="step_6__verify_that_full_page_heap_is_enabled"></span><span id="STEP_6__VERIFY_THAT_FULL_PAGE_HEAP_IS_ENABLED"></span>步骤6：验证是否已启用全页堆

以下命令列出为其启用页堆验证的程序：

```console
gflags /p
```

在响应中，GFlags 显示以下程序列表。 在此显示中，" **跟踪** " 指示标准页堆验证，而 " **完全跟踪** " 指示完全页堆验证。 在这种情况下，将列出 pheap-buggy.exe **完全跟踪**，指示已启用 "完全页堆验证"。

```console
pheap-buggy.exe: page heap enabled with flags (full traces )
```

### <a name="span-idstep_7__run_the_debugger_againspanspan-idstep_7__run_the_debugger_againspanspan-idstep_7__run_the_debugger_againspanstep-7-run-the-debugger-again"></a><span id="Step_7__Run_the_debugger_again"></span><span id="step_7__run_the_debugger_again"></span><span id="STEP_7__RUN_THE_DEBUGGER_AGAIN"></span>步骤7：再次运行调试器

以下命令在 NTSD 调试器中运行 pheap-buggy.exe 的 **CorruptAfterEnd** 函数，并使用 **-g** (忽略初始断点) ， **-x** (对访问冲突异常设置第二次中断) 参数：

```console
ntsd -g -x pheap-buggy CorruptAfterEnd
```

当应用程序失败时，NTSD 会生成以下显示，这表示它在 pheap-buggy.exe 检测到错误：

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

启用全页堆验证后，调试器将在出现访问冲突时中断。 若要确定访问冲突的确切位置，请打开行号转储，并显示 "调用堆栈" 跟踪。

编号调用堆栈跟踪如下所示： 

```console
ChildEBP RetAddr  Args to Child
0006ff3c 01001450 00000000 00000001 0006ffc0 pheap-buggy!TestCorruptAfterEnd+0x1f [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 184]
0006ff4c 0100157f 00000002 00c16fd0 00b70eb0 pheap-buggy!main+0xa9 [d:\nttest\base\testsrc\kernel\rtl\pageheap\pheap-buggy.cxx @ 69]
0006ffc0 77de43fe 00000000 00000001 7ffdf000 pheap-buggy!mainCRTStartup+0xe3 [crtexe.c @ 349]
WARNING: Stack unwind information not available. Following frames may be wrong.
0006fff0 00000000 0100149c 00000000 78746341 kernel32!DosPathToSessionPathA+0x204
```

堆栈跟踪显示问题发生在 pheap-buggy.exe 第184行。 由于启用了全页堆验证，因此调用堆栈在程序代码中启动，而不是在系统 DLL 中启动。 因此，冲突被捕获到了发生的位置，而不是释放堆块。

### <a name="span-idstep_8__locate_the_error_in_the_codespanspan-idstep_8__locate_the_error_in_the_codespanspan-idstep_8__locate_the_error_in_the_codespanstep-8-locate-the-error-in-the-code"></a><span id="Step_8__Locate_the_error_in_the_code"></span><span id="step_8__locate_the_error_in_the_code"></span><span id="STEP_8__LOCATE_THE_ERROR_IN_THE_CODE"></span>步骤8：在代码中找到错误

快速检查可揭示问题的原因：程序尝试写入256字节的257th 字节 (0x101)  (0x100) 缓冲区，这是一个常见的非一错误。

```console
*((PCHAR)Block + 0x100) = 0;
```

 

 





