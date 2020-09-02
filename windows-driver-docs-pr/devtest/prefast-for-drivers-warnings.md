---
title: 驱动程序的代码分析警告
description: 驱动程序的代码分析警告
ms.assetid: 61dba158-7e1b-42ee-9882-0ba9cef77b3c
keywords:
- PREfast for 驱动程序 WDK，警告
- 警告 WDK PREfast 驱动程序
- 错误 WDK PREfast 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efcb0ff623276522b783d6f3d5b33b8d0e6cf6ab
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382997"
---
# <a name="code-analysis-for-drivers-warnings"></a>驱动程序的代码分析警告


本部分列出并描述了驱动程序代码分析在检测到驱动程序代码中的错误时报告的警告。 请注意，某些警告适用于内核模式代码，分析用户模式驱动程序时，可以忽略这些警告。

驱动程序的代码分析报告以下类型的警告：

-   **一般警告** (6000-6999) ： c 和 c + + 语法中的潜在错误和常规编码做法。 有关这些警告的说明，请参阅 [C/c + + 的代码分析警告](/visualstudio/code-quality/code-analysis-for-c-cpp-warnings)。

-   **Windows 特定警告** (28600-28799) ：这些警告特定于 windows 中的某些模式，但并不特定于驱动程序。

-   **特定于驱动程序的警告** (28100-28199) ：驱动程序与应用程序的交互、其他驱动程序和操作系统之间的错误。

-   **批注错误** (28200-28299 和 36000-36999) ：这些警告表明批注未正确编码或在不正确的上下文中使用。 在大多数情况下，出现此类警告表明批注没有所需的 (或任何) 效果。

-   **内存分配警告** (30029-30035) ：这是内存分配警告。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="28101-wrong-function-type.md" data-raw-source="[C28101](28101-wrong-function-type.md)">C28101</a></p></td>
<td align="left"><p>警告 C28101：驱动程序模块已推断当前函数不是正确的函数类型</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28110-floating-point-hardware-protect.md" data-raw-source="[C28110](28110-floating-point-hardware-protect.md)">C28110</a></p></td>
<td align="left"><p>警告 C28110：驱动程序必须保护浮点硬件状态。 请参阅使用 float</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28111-floating-point-irql-mismatch.md" data-raw-source="[C28111](28111-floating-point-irql-mismatch.md)">C28111</a></p></td>
<td align="left"><p>警告 C28111：保存浮点状态的 IRQL 与当前 IRQL () 此还原操作不匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28114-improper-irp-stack-copy.md" data-raw-source="[C28114](28114-improper-irp-stack-copy.md)">C28114</a></p></td>
<td align="left"><p>警告： C28114：复制整个 IRP 堆栈条目会将某些字段初始化，应清除或更新这些字段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28120-irql-execution-too-low.md" data-raw-source="[C28120](28120-irql-execution-too-low.md)">C28120</a></p></td>
<td align="left"><p>警告 C28120：不允许在当前 IRQ 级别调用该函数。 当前级别过低。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28121-irq-execution-too-high.md" data-raw-source="[C28121](28121-irq-execution-too-high.md)">C28121</a></p></td>
<td align="left"><p>警告 C28121：不允许在当前 IRQ 级别调用该函数。 当前级别过高。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28122-inconsistent-irq-level-calls-low.md" data-raw-source="[C28122](28122-inconsistent-irq-level-calls-low.md)">C28122</a></p></td>
<td align="left"><p>警告 C28122：不允许在较低的 IRQ 级别调用该函数。 以前的函数调用与此约束不一致。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28123-inconsistent-irq-level-calls-high.md" data-raw-source="[C28123](28123-inconsistent-irq-level-calls-high.md)">C28123</a></p></td>
<td align="left"><p>警告 C28123：不允许在高 IRQ 级别调用此函数。 以前的函数调用与此约束不一致。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28124-call-below-minimum-irq-level.md" data-raw-source="[C28124](28124-call-below-minimum-irq-level.md)">C28124</a></p></td>
<td align="left"><p>警告 C28124：对的调用会导致 IRQ 级别设置为低于正在分析的函数可接受的最小值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28126-accessmode-param-incorrect.md" data-raw-source="[C28126](28126-accessmode-param-incorrect.md)">C28126</a></p></td>
<td align="left"><p>警告 C28126： ObReferenceObject * 的 AccessMode 参数应为 IRP- &gt; irp->requestormode</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28127-function-routine-mismatch.md" data-raw-source="[C28127](28127-function-routine-mismatch.md)">C28127</a></p></td>
<td align="left"><p>警告 C28127：用作例程的函数与预期类型不完全匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28128-structure-member-directly-accessed.md" data-raw-source="[C28128](28128-structure-member-directly-accessed.md)">C28128</a></p></td>
<td align="left"><p>警告 C28128：已直接访问字段。 它应由例程进行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28129-assignment-made-to-operand.md" data-raw-source="[C28129](28129-assignment-made-to-operand.md)">C28129</a></p></td>
<td align="left"><p>警告 C28129：已对操作数进行了赋值，只应使用位集进行修改并清除</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28131-driverentry-saving-pointer-to-buffer.md" data-raw-source="[C28131](28131-driverentry-saving-pointer-to-buffer.md)">C28131</a></p></td>
<td align="left"><p>警告 C28131： DriverEntry 例程应保存参数的副本，而不是指针，因为 i/o 管理器释放缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28132-driver-taking-the-size-of-pointer.md" data-raw-source="[C28132](28132-driver-taking-the-size-of-pointer.md)">C28132</a></p></td>
<td align="left"><p>警告 C28132：采用指针的大小</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28133-ioinitializetimer-is-best-called-from-add-device.md" data-raw-source="[C28133](28133-ioinitializetimer-is-best-called-from-add-device.md)">C28133</a></p></td>
<td align="left"><p>警告 C28133： IoInitializeTimer 最适用于 AddDevice</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28134-pool-tag-type-should-be-integral.md" data-raw-source="[C28134](28134-pool-tag-type-should-be-integral.md)">C28134</a></p></td>
<td align="left"><p>警告 C28134：池标记的类型应为整数，而不是字符串或字符串指针</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28135-first-argument-to-kewaitforsingleobject.md" data-raw-source="[C28135](28135-first-argument-to-kewaitforsingleobject.md)">C28135</a></p></td>
<td align="left"><p>警告 C28135：如果 KeWaitForSingleObject 的第一个参数是本地变量，则 Mode 参数必须为 KernelMode</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28139-argument-operand-should-exactly-match.md" data-raw-source="[C28139](28139-argument-operand-should-exactly-match.md)">C28139</a></p></td>
<td align="left"><p>警告 C28139：该参数应与类型完全匹配</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28141-argument-lowers-irq-level.md" data-raw-source="[C28141](28141-argument-lowers-irq-level.md)">C28141</a></p></td>
<td align="left"><p>警告 C28141：参数将导致 IRQ 级别设置为低于当前 IRQL，因此此函数无法用于该目的</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28143-iomarkirppending-must-return-statuspending.md" data-raw-source="[C28143](28143-iomarkirppending-must-return-statuspending.md)">C28143</a></p></td>
<td align="left"><p>警告 C28143：调用也的调度例程还必须返回 STATUS_PENDING</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28144-cancelirql-should-be-current-irql.md" data-raw-source="[C28144](28144-cancelirql-should-be-current-irql.md)">C28144</a></p></td>
<td align="left"><p>警告 C28144：在退出例程内，Irp 中的 IRQL- &gt; irp->cancelirql 应为当前 irql。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28145-opaque-mdl-structure-should-not-be-modified.md" data-raw-source="[C28145](28145-opaque-mdl-structure-should-not-be-modified.md)">C28145</a></p></td>
<td align="left"><p>警告 C28145：不透明 MDL 结构不应由驱动程序修改</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28146-kernel-mode-drivers-should-use-ntstrsafe.md" data-raw-source="[C28146](28146-kernel-mode-drivers-should-use-ntstrsafe.md)">C28146</a></p></td>
<td align="left"><p>警告 C28146：内核模式驱动程序应使用 ntstrsafe.h 而，而不是 strsafe。 在源文件中找到</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28147-improper-use-of-default-pool-tag.md" data-raw-source="[C28147](28147-improper-use-of-default-pool-tag.md)">C28147</a></p></td>
<td align="left"><p>警告 C28147： ) 对此函数的调用使用默认的池标记 ( "kdD" 或 "mdW"，因而无法实现池标记目的</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28150-function-causes-irq-level-to-be-set-above-max.md" data-raw-source="[C28150](28150-function-causes-irq-level-to-be-set-above-max.md)">C28150</a></p></td>
<td align="left"><p>警告 C28150：该函数导致 IRQ 级别设置为高于要分析的函数的最大可接受值</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28151-illegal-irql-value.md" data-raw-source="[C28151](28151-illegal-irql-value.md)">C28151</a></p></td>
<td align="left"><p>警告 C28151：值不是有效值的有效值</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28152-do-device-initializing-flag-not-cleared.md" data-raw-source="[C28152](28152-do-device-initializing-flag-not-cleared.md)">C28152</a></p></td>
<td align="left"><p>警告 C28152：意外地从 AddDevice 函数返回 DO_DEVICE_INITIALIZING</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28153-irql-annotation-eval-context.md" data-raw-source="[C28153](28153-irql-annotation-eval-context.md)">C28153</a></p></td>
<td align="left"><p>警告 C28153：在此上下文中无法计算来自批注的 IRQL 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28156-irql-inconsistent-with-required-irq-value.md" data-raw-source="[C28156](28156-irql-inconsistent-with-required-irq-value.md)">C28156</a></p></td>
<td align="left"><p>警告 C28156：实际的 IRQL 与所需 IRQL 不一致</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28157-function-irql-never-restored.md" data-raw-source="[C28157](28157-function-irql-never-restored.md)">C28157</a></p></td>
<td align="left"><p>警告 C28157：不还原 IRQL</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28158-no-irql-was-saved.md" data-raw-source="[C28158](28158-no-irql-was-saved.md)">C28158</a></p></td>
<td align="left"><p>警告 C28158：未保存 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28161-exiting-without-right-to-use-floating-hardware.md" data-raw-source="[C28161](28161-exiting-without-right-to-use-floating-hardware.md)">C28161</a></p></td>
<td align="left"><p>警告 C28161：在未获取使用浮动硬件的权限的情况下退出</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28162-exiting-while-holding-right-to-use-floating-hardware.md" data-raw-source="[C28162](28162-exiting-while-holding-right-to-use-floating-hardware.md)">C28162</a></p></td>
<td align="left"><p>警告 C28162：在持有使用浮点硬件的权利时退出</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28165-class-function-pointer-mismatch.md" data-raw-source="[C28165](28165-class-function-pointer-mismatch.md)">C28165</a></p></td>
<td align="left"><p>警告 C28165：类的函数指针与函数类不匹配</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28166-function-does-not-restore-irql-value.md" data-raw-source="[C28166](28166-function-does-not-restore-irql-value.md)">C28166</a></p></td>
<td align="left"><p>警告 C28166：该函数不会将 IRQL 恢复为当前位于函数入口的值，并且此操作是必需的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28167-function-changes-irql-without-restore.md" data-raw-source="[C28167](28167-function-changes-irql-without-restore.md)">C28167</a></p></td>
<td align="left"><p>警告 C28167：该函数更改 IRQL，不会在其退出之前还原 IRQL。 应对其进行批注，以反映更改或应还原 IRQL。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28168-dispatch-function-dispatch-annotation.md" data-raw-source="[C28168](28168-dispatch-function-dispatch-annotation.md)">C28168</a></p></td>
<td align="left"><p>警告 C28168：调度函数没有与此调度表项匹配的 <strong><em>Dispatch_type</em></strong> 批注</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28169-dispatch-function-does-not-have-proper-annotation.md" data-raw-source="[C28169](28169-dispatch-function-does-not-have-proper-annotation.md)">C28169</a></p></td>
<td align="left"><p>警告 C28169：调度函数没有任何 <strong><em>Dispatch_type</em></strong> 批注</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28170-pageable-code-macro-not-found.md" data-raw-source="[C28170](28170-pageable-code-macro-not-found.md)">C28170</a></p></td>
<td align="left"><p>警告 C28170：该函数已被声明为位于分页段中，但找不到 PAGED_CODE 和 PAGED_CODE_LOCKED</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28171-function-has-more-than-one-page-macro-instance.md" data-raw-source="[C28171](28171-function-has-more-than-one-page-macro-instance.md)">C28171</a></p></td>
<td align="left"><p>警告 C28171：该函数有多个 PAGED_CODE 或 PAGED_CODE_LOCKED 的实例</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28172-function-macros-not-in-paged-segment.md" data-raw-source="[C28172](28172-function-macros-not-in-paged-segment.md)">C28172</a></p></td>
<td align="left"><p>警告 C28172：该函数有 PAGED_CODE 或 PAGED_CODE_LOCKED，但未被声明为位于分页段中</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28173-function-incorrectly-adapts-to-memory-above-4gb.md" data-raw-source="[C28173](28173-function-incorrectly-adapts-to-memory-above-4gb.md)">C28173</a></p></td>
<td align="left"><p>警告 C28173：当前函数似乎错误地适应大于 4 GB 的物理内存</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28175struct-member-should-not-be-accessed-by-driver.md" data-raw-source="[C28175](28175struct-member-should-not-be-accessed-by-driver.md)">C28175</a></p></td>
<td align="left"><p>警告 C28175：结构的成员不应由驱动程序访问</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28176-struct-member-should-not-be-modified-by-driver.md" data-raw-source="[C28176](28176-struct-member-should-not-be-modified-by-driver.md)">C28176</a></p></td>
<td align="left"><p>警告 C28176：结构的成员不应由驱动程序修改</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28177-function-annotated-with-more-than-one-class.md" data-raw-source="[C28177](28177-function-annotated-with-more-than-one-class.md)">C28177</a></p></td>
<td align="left"><p>警告 C28177：函数已用多个函数类进行批注。 除一个以外的所有项都将被忽略。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28260-syntax-error-in-function-property.md" data-raw-source="[C28260](28260-syntax-error-in-function-property.md)">C28260</a></p></td>
<td align="left"><p>警告 C28260：分析函数内的属性时，在注释中发现了语法错误</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28266-function-property-syntax-error.md" data-raw-source="[C28266](28266-function-property-syntax-error.md)">C28266</a></p></td>
<td align="left"><p>在函数中找到了批注的语法错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28268-function-class-does-not-match-typedef.md" data-raw-source="[C28268](28268-function-class-does-not-match-typedef.md)">C28268</a></p></td>
<td align="left"><p>警告 C28268：函数的函数类与此处使用的 typedef 上的函数类不匹配</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28601-avoid-blocking-on-hwnd-broadcast.md" data-raw-source="[C28601](28601-avoid-blocking-on-hwnd-broadcast.md)">C28601</a></p></td>
<td align="left"><p>警告 C28601：避免阻塞 HWND_BROADCAST</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28602-avoid-calling-sendmessagetimeout-with-hwnd-broadcast.md" data-raw-source="[C28602](28602-avoid-calling-sendmessagetimeout-with-hwnd-broadcast.md)">C28602</a></p></td>
<td align="left"><p>警告 C28602：避免调用带有 HWND_BROADCAST 的 SendMessageTimeout</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28604-smto-abortifhung-with-0-timeout-.md" data-raw-source="[C28604](28604-smto-abortifhung-with-0-timeout-.md)">C28604</a></p></td>
<td align="left"><p>警告 C28604：避免使用超时值为0的 SMTO_ABORTIFHUNG 调用 SendMessageTimeout</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28615-must-call-resetstkoflw-in-except-block.md" data-raw-source="[C28615](28615-must-call-resetstkoflw-in-except-block.md)">C28615</a></p></td>
<td align="left"><p>警告 C28615： __except 在 __try 块中调用 _alloca 时，必须在 ( # A1 块中调用 _resetstkoflw。 不要从 catch ( # A1 块内调用 _resetstkoflw</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28616-multithreaded-av-condition.md" data-raw-source="[C28616](28616-multithreaded-av-condition.md)">C28616</a></p></td>
<td align="left"><p>警告 C28616：多线程 AV 条件</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28617-avoid-using-the-return-value-of-beginthread.md" data-raw-source="[C28617](28617-avoid-using-the-return-value-of-beginthread.md)">C28617</a></p></td>
<td align="left"><p>警告 C28617：避免使用 ( # A1 _beginthread 的返回值。 改用 _beginthreadex ( # A1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28623-unsigned-cast-of-getmessagepos-coordinates.md" data-raw-source="[C28623](28623-unsigned-cast-of-getmessagepos-coordinates.md)">C28623</a></p></td>
<td align="left"><p>警告 C28623： GetMessagePos ( # A1 坐标的未签名强制转换。 使用 GET_X_LPARAM/GET_Y_LPARAM 而不是 LOWORD/HIWORD</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28624-no-release-call-to-match-incremented-refcount.md" data-raw-source="[C28624](28624-no-release-call-to-match-incremented-refcount.md)">C28624</a></p></td>
<td align="left"><p>警告 C28624：不调用 Release ( # A1，以匹配 LResultFromObject 中的递增引用计数</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28625-sensitive-data-may-be-retained.md" data-raw-source="[C28625](28625-sensitive-data-may-be-retained.md)">C28625</a></p></td>
<td align="left"><p>警告 C28625：用于清除敏感数据的函数调用将被优化掉</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28636-calling-localfree-on-non-allocated-pointer.md" data-raw-source="[C28636](28636-calling-localfree-on-non-allocated-pointer.md)">C28636</a></p></td>
<td align="left"><p>警告 C28636：在通过调用 GetSecurityDescriptorOwner/Group/Dacl/Sacl 获取的非分配指针上调用 LocalFree</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28637-calling-function-in-a-global-initializer-is-unsafe.md" data-raw-source="[C28637](28637-calling-function-in-a-global-initializer-is-unsafe.md)">C28637</a></p></td>
<td align="left"><p>警告 C28637：在全局初始值设定项中调用函数是不安全的</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28638-function-delayload-stub-is-missing-declaration-.md" data-raw-source="[C28638](28638-function-delayload-stub-is-missing-declaration-.md)">C28638</a></p></td>
<td align="left"><p>警告 C28638：函数延迟加载存根缺少匹配的声明</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28639-calling-close-handle-with-string.md" data-raw-source="[C28639](28639-calling-close-handle-with-string.md)">C28639</a></p></td>
<td align="left"><p>警告 C28639：正在用字符串调用关闭句柄</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28640-delayload-function-stub-should-be-a-static-function.md" data-raw-source="[C28640](28640-delayload-function-stub-should-be-a-static-function.md)">C28640</a></p></td>
<td align="left"><p>警告 C28640：函数延迟加载存根应为静态函数</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28644-return-value-from-dpa-insertptr-not-checked.md" data-raw-source="[C28644](28644-return-value-from-dpa-insertptr-not-checked.md)">C28644</a></p></td>
<td align="left"><p>警告 C28644：未选中 DPA_InsertPtr 的返回值</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28645-messagebox-called-using-the-question-mark-symbol.md" data-raw-source="[C28645](28645-messagebox-called-using-the-question-mark-symbol.md)">C28645</a></p></td>
<td align="left"><p>警告 C28645：使用不再推荐的问号消息符号调用了 MessageBox</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28648-pulseevent-is-an-unreliable-function.md" data-raw-source="[C28648](28648-pulseevent-is-an-unreliable-function.md)">C28648</a></p></td>
<td align="left"><p>警告 C28648： PulseEvent 是不可靠的函数</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28649-automatic-or-global-stack-arrays-are-never-null.md" data-raw-source="[C28649](28649-automatic-or-global-stack-arrays-are-never-null.md)">C28649</a></p></td>
<td align="left"><p>警告 C28649：自动或全局堆栈数组始终不为 NULL</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28650-generic-value-is-not-treated-as-failure.md" data-raw-source="[C28650](28650-generic-value-is-not-treated-as-failure.md)">C28650</a></p></td>
<td align="left"><p>警告 C28650：使用！0的类型不会将其视为故障情况。</p>
<p>返回状态值，如！TRUE 与返回指示失败的状态值的值不同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28651-member-function-pointers-cause-write-pages-copy.md" data-raw-source="[C28651](28651-member-function-pointers-cause-write-pages-copy.md)">C28651</a></p></td>
<td align="left"><p>警告 C28651：静态初始值设定项导致在写入页上复制，原因是成员函数指针</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28652-overloaded-bitwise-operators-cause-write-pages-copy.md" data-raw-source="[C28652](28652-overloaded-bitwise-operators-cause-write-pages-copy.md)">C28652</a></p></td>
<td align="left"><p>警告 C28652：由于重载的按位运算符，静态初始值设定项导致写入页上的副本</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28714-ntstatus-cast-between-semantically-different-integer-types.md" data-raw-source="[C28714](28714-ntstatus-cast-between-semantically-different-integer-types.md)">C28714</a></p></td>
<td align="left"><p>警告 C28714：语义不同的整数类型之间的强制转换</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28715-boolean-cast-between-semantically-different-integer-types.md" data-raw-source="[C28715](28715-boolean-cast-between-semantically-different-integer-types.md)">C28715</a></p></td>
<td align="left"><p>警告 C28715：语义不同的整数类型之间的强制转换</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28716-compiler-inserted-cast-between-semantically-different-integral.md" data-raw-source="[C28716](28716-compiler-inserted-cast-between-semantically-different-integral.md)">C28716</a></p></td>
<td align="left"><p>警告 C28716：在语义不同的整数类型之间进行编译器插入的强制转换</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28717-invalid-variant-type.md" data-raw-source="[C28717](28717-invalid-variant-type.md)">C28717</a></p></td>
<td align="left"><p>警告 C28717：无效的 VARIANT 类型</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28718-unannotated-buffer.md" data-raw-source="[C28718](28718-unannotated-buffer.md)">C28718</a></p></td>
<td align="left"><p>警告 C28718：批注缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28719-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28719](28719-banned-api-usage-use-updated-function-replacement.md)">C28719</a></p></td>
<td align="left"><p>警告 C28719：已禁止的 API 用法</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28720-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28720](28720-banned-api-usage-use-updated-function-replacement.md)">C28720</a></p></td>
<td align="left"><p>警告 C28720：已禁止的 API 用法</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28721-deprecated-performance-counter-architecture.md" data-raw-source="[C28721](28721-deprecated-performance-counter-architecture.md)">C28721</a></p></td>
<td align="left"><p>警告 C28721：已弃用的性能计数器体系结构</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28722-unannotated-function-declaration-buffer.md" data-raw-source="[C28722](28722-unannotated-function-declaration-buffer.md)">C28722</a></p></td>
<td align="left"><p>警告 C28722：函数声明中的批注缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28723-unannotated-buffer-without-declaration.md" data-raw-source="[C28723](28723-unannotated-buffer-without-declaration.md)">C28723</a></p></td>
<td align="left"><p>警告 C28723：在函数定义中没有相应声明的批注缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28725-use-watson-instead.md" data-raw-source="[C28725](28725-use-watson-instead.md)">C28725</a></p></td>
<td align="left"><p>警告 C28725：使用 Watson 而不是此 SetUnhandledExceptionFilter</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28726-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28726](28726-banned-api-usage-use-updated-function-replacement.md)">C28726</a></p></td>
<td align="left"><p>警告 C28726：已禁止的 API 用法</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28727-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28727](28727-banned-api-usage-use-updated-function-replacement.md)">C28727</a></p></td>
<td align="left"><p>警告 C28727：已禁止的 API 用法</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28728-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28728](28728-banned-api-usage-use-updated-function-replacement.md)">C28728</a></p></td>
<td align="left"><p>警告 C28728：已禁止的 API 用法</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28730-possible-null-character-assignment.md" data-raw-source="[C28730](28730-possible-null-character-assignment.md)">C28730</a></p></td>
<td align="left"><p>警告 C28730：可能会直接将 "\ 0" 分配给指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28735-banned-crimson-api-usage.md" data-raw-source="[C28735](28735-banned-crimson-api-usage.md)">C28735</a></p></td>
<td align="left"><p>警告 C28735：禁止 Crimson API 使用情况</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28736-legacy-crimson-or-perflib-banned-argument-used.md" data-raw-source="[C28736](28736-legacy-crimson-or-perflib-banned-argument-used.md)">C28736</a></p></td>
<td align="left"><p>警告 C28736：已禁止的 API 参数用法</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28740-unannotated-unsigned-buffer.md" data-raw-source="[C28740](28740-unannotated-unsigned-buffer.md)">C28740</a></p></td>
<td align="left"><p>警告 C28740：批注无符号缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28741-unannotated-non-constant-string-buffer-in-function.md" data-raw-source="[C28741](28741-unannotated-non-constant-string-buffer-in-function.md)">C28741</a></p></td>
<td align="left"><p>警告 C28741：函数中的批注缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28742-unnanotated-non-constant-buffer-in-function.md" data-raw-source="[C28742](28742-unnanotated-non-constant-buffer-in-function.md)">C28742</a></p></td>
<td align="left"><p>警告 C28742：函数中的批注缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28750-banned-istrlen-usage.md" data-raw-source="[C28750](28750-banned-istrlen-usage.md)">C28750</a></p></td>
<td align="left"><p>警告 C28750： lstrlen 及其变体的禁止使用情况</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28751-banned-exallocatepool-usage.md" data-raw-source="[C28751](28751-banned-exallocatepool-usage.md)">C28751</a></p></td>
<td align="left"><p>警告 C28751： ExAllocatePool 及其变体的禁止使用情况</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28752-banned-kernel32-advapi32-usage.md" data-raw-source="[C28752](28752-banned-kernel32-advapi32-usage.md)">C28752</a></p></td>
<td align="left"><p>警告 C28752： kernel32.dll 或 advapi32.dll API 的禁止使用</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28753-relying-on-undefined-order-of-evalutation-params.md" data-raw-source="[C28753](28753-relying-on-undefined-order-of-evalutation-params.md)">C28753</a></p></td>
<td align="left"><p>警告 C28753：依赖于未定义的参数计算顺序</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30029-memory-allocating-function-requests-executable-memory.md" data-raw-source="[C30029](30029-memory-allocating-function-requests-executable-memory.md)">C30029</a></p></td>
<td align="left"><p>警告 C30029：调用请求可执行内存的内存分配函数</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="30030-parameter-indicates-executable-memory.md" data-raw-source="[C30030](30030-parameter-indicates-executable-memory.md)">C30030</a></p></td>
<td align="left"><p>警告 C30030：调用内存分配函数并传递指示可执行内存的参数</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30031-pool-n-optin-called-before-entry-function.md" data-raw-source="[C30031](30031-pool-n-optin-called-before-entry-function.md)">C30031</a></p></td>
<td align="left"><p>警告 C30031：调用内存分配函数并传递指示可执行内存的参数</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="30032-forcing-request-of-executable-memory.md" data-raw-source="[C30032](30032-forcing-request-of-executable-memory.md)">C30032</a></p></td>
<td align="left"><p>警告 C30032：调用内存分配函数并通过使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/selective-opt-out-pool-nx-optout" data-raw-source="[POOL_NX_OPTOUT](../kernel/selective-opt-out-pool-nx-optout.md)">POOL_NX_OPTOUT</a> 指令强制执行可执行内存请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30033-executable-allocation-detected-with-pool-nx-optin.md" data-raw-source="[C30033](30033-executable-allocation-detected-with-pool-nx-optin.md)">C30033</a></p></td>
<td align="left"><p>警告 C30033：在使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/single-binary-opt-in-pool-nx-optin" data-raw-source="[POOL_NX_OPTIN](../kernel/single-binary-opt-in-pool-nx-optin.md)">POOL_NX_OPTIN</a>编译的驱动程序中检测到可执行分配。 已确定此驱动程序在运行时由另一个驱动程序加载。 请验证加载驱动程序是否在其 DriverEntry 中调用了 <strong>ExInitializeDriverRuntime (<em>DrvRtPoolNxOptIn</em>) </strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="30034-passing-flag-value-to-allocating-function.md" data-raw-source="[C30034](30034-passing-flag-value-to-allocating-function.md)">C30034</a></p></td>
<td align="left"><p>警告 C30034：将标志值传递给可能导致分配可执行内存的分配函数。 请验证分配函数未请求可执行的非分页池的形式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30035-function-call-must-be-made-inside-init-function.md" data-raw-source="[C30035](30035-function-call-must-be-made-inside-init-function.md)">C30035</a></p></td>
<td align="left"><p>警告 C30035：调用了一个函数，该函数必须在初始化函数内进行 (例如， <strong>DriverEntry ( # B2 </strong> 或 <strong>DllInitialize ( # B4 </strong>) 。 PREfast 无法确定是否从初始化函数进行调用。</p></td>
</tr>
</tbody>
</table>

 

 

