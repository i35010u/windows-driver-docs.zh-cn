---
title: 代码分析驱动程序警告
description: 代码分析驱动程序警告
ms.assetid: 61dba158-7e1b-42ee-9882-0ba9cef77b3c
keywords:
- PREfast 驱动程序 WDK，警告
- 警告 WDK PREfast for Drivers
- 错误 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dba77475c1343f224052fde589037e4af12bb47e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555728"
---
# <a name="code-analysis-for-drivers-warnings"></a>代码分析驱动程序警告


本部分列出并描述当驱动程序代码中检测到可能的错误时，Code Analysis for Drivers 报告的警告。 请注意，一些警告，适用于内核模式代码分析用户模式驱动程序时可以忽略。

驱动程序的代码分析报告的警告的以下类型：

-   **常规警告**(6000 6999):在 C 和 c + + 语法和一般的编码实践的潜在错误。 有关这些警告的说明，请参阅[的代码分析 C/c + + 警告](/visualstudio/code-quality/code-analysis-for-c-cpp-warnings)。

-   **Windows 特定警告**(28600 28799):这些警告特定于 Windows，在使用某些模式，但并不特定于驱动程序。

-   **特定于驱动程序警告**(28100 28199):应用程序、 其他驱动程序和操作系统的驱动程序的交互中存在错误。

-   **批注错误**（28200 28299 和 36000 36999）：这些警告表明批注具有已正确编码的或不正确的上下文中使用。 在大多数情况下，是否存在这样的警告指示所需 （或者任何），批注不会出现的效果。

-   **内存分配警告**(为 30029 30035):这些是分配的内存警告。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>在本部分中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="28101-wrong-function-type.md" data-raw-source="[C28101](28101-wrong-function-type.md)">C28101</a></p></td>
<td align="left"><p>警告 C28101:驱动程序模块已推断当前函数不是正确的函数类型</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28110-floating-point-hardware-protect.md" data-raw-source="[C28110](28110-floating-point-hardware-protect.md)">C28110</a></p></td>
<td align="left"><p>警告 C28110:驱动程序必须保护浮点硬件状态。 请参阅使用 float</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28111-floating-point-irql-mismatch.md" data-raw-source="[C28111](28111-floating-point-irql-mismatch.md)">C28111</a></p></td>
<td align="left"><p>警告 C28111:保存浮点状态的 IRQL 与当前 IRQL （适用于此恢复操作） 不匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28114-improper-irp-stack-copy.md" data-raw-source="[C28114](28114-improper-irp-stack-copy.md)">C28114</a></p></td>
<td align="left"><p>警告：C28114:复制整个 IRP 堆栈条目离开初始化，应清除或更新某些字段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28120-irql-execution-too-low.md" data-raw-source="[C28120](28120-irql-execution-too-low.md)">C28120</a></p></td>
<td align="left"><p>警告 C28120:不允许在当前 IRQ 级别调用该函数。 当前级别过低。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28121-irq-execution-too-high.md" data-raw-source="[C28121](28121-irq-execution-too-high.md)">C28121</a></p></td>
<td align="left"><p>警告 C28121:不允许在当前 IRQ 级别调用该函数。 当前级别过高。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28122-inconsistent-irq-level-calls-low.md" data-raw-source="[C28122](28122-inconsistent-irq-level-calls-low.md)">C28122</a></p></td>
<td align="left"><p>警告 C28122:不允许在较低的 IRQ 级别调用该函数。 以前的函数调用是与此约束不一致。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28123-inconsistent-irq-level-calls-high.md" data-raw-source="[C28123](28123-inconsistent-irq-level-calls-high.md)">C28123</a></p></td>
<td align="left"><p>警告 C28123:不允许在较高的 IRQ 级别调用该函数。 以前的函数调用是与此约束不一致。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28124-call-below-minimum-irq-level.md" data-raw-source="[C28124](28124-call-below-minimum-irq-level.md)">C28124</a></p></td>
<td align="left"><p>警告 C28124:对的调用会导致 IRQ 级别要低于最小值设置为所分析函数可接受。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28126-accessmode-param-incorrect.md" data-raw-source="[C28126](28126-accessmode-param-incorrect.md)">C28126</a></p></td>
<td align="left"><p>警告 C28126:ObReferenceObject * 的 AccessMode 参数应为 IRP-&gt;RequestorMode</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28127-function-routine-mismatch.md" data-raw-source="[C28127](28127-function-routine-mismatch.md)">C28127</a></p></td>
<td align="left"><p>警告 C28127:作为例程所使用的函数与预期的类型不完全匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28128-structure-member-directly-accessed.md" data-raw-source="[C28128](28128-structure-member-directly-accessed.md)">C28128</a></p></td>
<td align="left"><p>警告 C28128:已直接进行访问的字段。 它应该是通过例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28129-assignment-made-to-operand.md" data-raw-source="[C28129](28129-assignment-made-to-operand.md)">C28129</a></p></td>
<td align="left"><p>警告 C28129:分配对操作数，应仅修改使用位设置和清除</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28131-driverentry-saving-pointer-to-buffer.md" data-raw-source="[C28131](28131-driverentry-saving-pointer-to-buffer.md)">C28131</a></p></td>
<td align="left"><p>警告 C28131:DriverEntry 例程应保存一份参数，而不是指针，因为 I/O 管理器释放缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28132-driver-taking-the-size-of-pointer.md" data-raw-source="[C28132](28132-driver-taking-the-size-of-pointer.md)">C28132</a></p></td>
<td align="left"><p>警告 C28132:获取指针的大小</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28133-ioinitializetimer-is-best-called-from-add-device.md" data-raw-source="[C28133](28133-ioinitializetimer-is-best-called-from-add-device.md)">C28133</a></p></td>
<td align="left"><p>警告 C28133:最好最好从 AddDevice 调用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28134-pool-tag-type-should-be-integral.md" data-raw-source="[C28134](28134-pool-tag-type-should-be-integral.md)">C28134</a></p></td>
<td align="left"><p>警告 C28134:池标记的类型应整型，而不是字符串或字符串指针</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28135-first-argument-to-kewaitforsingleobject.md" data-raw-source="[C28135](28135-first-argument-to-kewaitforsingleobject.md)">C28135</a></p></td>
<td align="left"><p>警告 C28135:如果 KeWaitForSingleObject 的第一个参数是本地变量，则 Mode 参数必须为 KernelMode</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28139-argument-operand-should-exactly-match.md" data-raw-source="[C28139](28139-argument-operand-should-exactly-match.md)">C28139</a></p></td>
<td align="left"><p>警告 C28139:参数应与类型完全匹配</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28141-argument-lowers-irq-level.md" data-raw-source="[C28141](28141-argument-lowers-irq-level.md)">C28141</a></p></td>
<td align="left"><p>警告 C28141:该参数导致 IRQ 级别设置低于当前 irql，因此，此函数不能用于此目的</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28143-iomarkirppending-must-return-statuspending.md" data-raw-source="[C28143](28143-iomarkirppending-must-return-statuspending.md)">C28143</a></p></td>
<td align="left"><p>警告 C28143:调用的调度例程也必须返回 STATUS_PENDING</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28144-cancelirql-should-be-current-irql.md" data-raw-source="[C28144](28144-cancelirql-should-be-current-irql.md)">C28144</a></p></td>
<td align="left"><p>警告 C28144:在取消例程，退出，在 Irp 的 IRQL&gt;CancelIrql 应为当前 IRQL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28145-opaque-mdl-structure-should-not-be-modified.md" data-raw-source="[C28145](28145-opaque-mdl-structure-should-not-be-modified.md)">C28145</a></p></td>
<td align="left"><p>警告 C28145:不透明 MDL 结构不应修改由驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28146-kernel-mode-drivers-should-use-ntstrsafe.md" data-raw-source="[C28146](28146-kernel-mode-drivers-should-use-ntstrsafe.md)">C28146</a></p></td>
<td align="left"><p>警告 C28146:内核模式驱动程序应使用 ntstrsafe.h，不 strsafe.h。 在源文件中找到</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28147-improper-use-of-default-pool-tag.md" data-raw-source="[C28147](28147-improper-use-of-default-pool-tag.md)">C28147</a></p></td>
<td align="left"><p>警告 C28147:使用默认的池标记 (&#39; kdD&#39;或&#39;mdW&#39;) 调用此函数无法实现标记池的用途</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28150-function-causes-irq-level-to-be-set-above-max.md" data-raw-source="[C28150](28150-function-causes-irq-level-to-be-set-above-max.md)">C28150</a></p></td>
<td align="left"><p>警告 C28150:该函数导致 IRQ 级别设置高于最大值为所分析函数可接受</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28151-illegal-irql-value.md" data-raw-source="[C28151](28151-illegal-irql-value.md)">C28151</a></p></td>
<td align="left"><p>警告 C28151:值不是合法的 IRQL 值</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28152-do-device-initializing-flag-not-cleared.md" data-raw-source="[C28152](28152-do-device-initializing-flag-not-cleared.md)">C28152</a></p></td>
<td align="left"><p>警告 C28152:从类似 AddDevice 的函数返回意外 DO_DEVICE_INITIALIZING</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28153-irql-annotation-eval-context.md" data-raw-source="[C28153](28153-irql-annotation-eval-context.md)">C28153</a></p></td>
<td align="left"><p>警告 C28153:无法在此上下文中计算 IRQL 从批注的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28156-irql-inconsistent-with-required-irq-value.md" data-raw-source="[C28156](28156-irql-inconsistent-with-required-irq-value.md)">C28156</a></p></td>
<td align="left"><p>警告 C28156:实际 IRQL 是与所需的 IRQL 不一致</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28157-function-irql-never-restored.md" data-raw-source="[C28157](28157-function-irql-never-restored.md)">C28157</a></p></td>
<td align="left"><p>警告 C28157:IRQL 从未恢复</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28158-no-irql-was-saved.md" data-raw-source="[C28158](28158-no-irql-was-saved.md)">C28158</a></p></td>
<td align="left"><p>警告 C28158:未保存 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28161-exiting-without-right-to-use-floating-hardware.md" data-raw-source="[C28161](28161-exiting-without-right-to-use-floating-hardware.md)">C28161</a></p></td>
<td align="left"><p>警告 C28161:正在退出而不获取使用浮点硬件的权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28162-exiting-while-holding-right-to-use-floating-hardware.md" data-raw-source="[C28162](28162-exiting-while-holding-right-to-use-floating-hardware.md)">C28162</a></p></td>
<td align="left"><p>警告 C28162:退出同时保留使用浮点硬件的权限</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28165-class-function-pointer-mismatch.md" data-raw-source="[C28165](28165-class-function-pointer-mismatch.md)">C28165</a></p></td>
<td align="left"><p>警告 C28165:类的函数指针与函数类不匹配</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28166-function-does-not-restore-irql-value.md" data-raw-source="[C28166](28166-function-does-not-restore-irql-value.md)">C28166</a></p></td>
<td align="left"><p>警告 C28166:该函数不会将 irql 恢复为当前位于函数入口和执行此操作所需的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28167-function-changes-irql-without-restore.md" data-raw-source="[C28167](28167-function-changes-irql-without-restore.md)">C28167</a></p></td>
<td align="left"><p>警告 C28167:该函数更改的 IRQL，并在退出之前不会还原 IRQL。 它应添加批注以反映此更改或 IRQL 应还原。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28168-dispatch-function-dispatch-annotation.md" data-raw-source="[C28168](28168-dispatch-function-dispatch-annotation.md)">C28168</a></p></td>
<td align="left"><p>警告 C28168:调度函数没有<strong><em>Dispatch_type</em></strong>批注匹配此调度表条目</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28169-dispatch-function-does-not-have-proper-annotation.md" data-raw-source="[C28169](28169-dispatch-function-does-not-have-proper-annotation.md)">C28169</a></p></td>
<td align="left"><p>警告 C28169:调度函数没有任何<strong><em>Dispatch_type</em></strong>批注</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28170-pageable-code-macro-not-found.md" data-raw-source="[C28170](28170-pageable-code-macro-not-found.md)">C28170</a></p></td>
<td align="left"><p>警告 C28170:该函数具有声明位于分页段中，但找到 PAGED_CODE 或 PAGED_CODE_LOCKED 既不</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28171-function-has-more-than-one-page-macro-instance.md" data-raw-source="[C28171](28171-function-has-more-than-one-page-macro-instance.md)">C28171</a></p></td>
<td align="left"><p>警告 C28171:该函数具有 PAGED_CODE 或 PAGED_CODE_LOCKED 的多个实例</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28172-function-macros-not-in-paged-segment.md" data-raw-source="[C28172](28172-function-macros-not-in-paged-segment.md)">C28172</a></p></td>
<td align="left"><p>警告 C28172:该函数具有 PAGED_CODE 或 PAGED_CODE_LOCKED，但未声明位于分页段</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28173-function-incorrectly-adapts-to-memory-above-4gb.md" data-raw-source="[C28173](28173-function-incorrectly-adapts-to-memory-above-4gb.md)">C28173</a></p></td>
<td align="left"><p>警告 C28173:当前函数似乎错误地适应 4GB 以上的物理内存</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28175struct-member-should-not-be-accessed-by-driver.md" data-raw-source="[C28175](28175struct-member-should-not-be-accessed-by-driver.md)">C28175</a></p></td>
<td align="left"><p>警告 C28175:结构的成员不应访问由驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28176-struct-member-should-not-be-modified-by-driver.md" data-raw-source="[C28176](28176-struct-member-should-not-be-modified-by-driver.md)">C28176</a></p></td>
<td align="left"><p>警告 C28176:结构的成员不应修改由驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28177-function-annotated-with-more-than-one-class.md" data-raw-source="[C28177](28177-function-annotated-with-more-than-one-class.md)">C28177</a></p></td>
<td align="left"><p>警告 C28177:函数将多个函数类批注。 除其中一个将被忽略。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28260-syntax-error-in-function-property.md" data-raw-source="[C28260](28260-syntax-error-in-function-property.md)">C28260</a></p></td>
<td align="left"><p>警告 C28260:在函数内的属性进行分析时找到批注中的语法错误</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28266-function-property-syntax-error.md" data-raw-source="[C28266](28266-function-property-syntax-error.md)">C28266</a></p></td>
<td align="left"><p>函数中的属性找到批注中的语法错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28268-function-class-does-not-match-typedef.md" data-raw-source="[C28268](28268-function-class-does-not-match-typedef.md)">C28268</a></p></td>
<td align="left"><p>警告 C28268:针对函数的函数类与此处使用的 typedef 上的函数类不匹配</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28601-avoid-blocking-on-hwnd-broadcast.md" data-raw-source="[C28601](28601-avoid-blocking-on-hwnd-broadcast.md)">C28601</a></p></td>
<td align="left"><p>警告 C28601:避免在 HWND_BROADCAST 上发生阻塞</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28602-avoid-calling-sendmessagetimeout-with-hwnd-broadcast.md" data-raw-source="[C28602](28602-avoid-calling-sendmessagetimeout-with-hwnd-broadcast.md)">C28602</a></p></td>
<td align="left"><p>警告 C28602:避免使用 HWND_BROADCAST 调用 SendMessageTimeout</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28604-smto-abortifhung-with-0-timeout-.md" data-raw-source="[C28604](28604-smto-abortifhung-with-0-timeout-.md)">C28604</a></p></td>
<td align="left"><p>警告 C28604:避免使用 SMTO_ABORTIFHUNG 调用 SendMessageTimeout 超时值为 0</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28615-must-call-resetstkoflw-in-except-block.md" data-raw-source="[C28615](28615-must-call-resetstkoflw-in-except-block.md)">C28615</a></p></td>
<td align="left"><p>警告 C28615:必须在 __except 块中调用 _resetstkoflw，__try 块中调用 _alloca 时。 Don&#39;从 catch （） 块内的 t 调用 _resetstkoflw</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28616-multithreaded-av-condition.md" data-raw-source="[C28616](28616-multithreaded-av-condition.md)">C28616</a></p></td>
<td align="left"><p>警告 C28616:多线程的 AV 条件</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28617-avoid-using-the-return-value-of-beginthread.md" data-raw-source="[C28617](28617-avoid-using-the-return-value-of-beginthread.md)">C28617</a></p></td>
<td align="left"><p>警告 C28617:避免使用 _beginthread （） 返回的值。 而是使用 _beginthreadex （）</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28623-unsigned-cast-of-getmessagepos-coordinates.md" data-raw-source="[C28623](28623-unsigned-cast-of-getmessagepos-coordinates.md)">C28623</a></p></td>
<td align="left"><p>警告 C28623:无符号强制转换 GetMessagePos() 坐标。 使用 GET_X_LPARAM/GET_Y_LPARAM，而不是使用 LOWORD/HIWORD</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28624-no-release-call-to-match-incremented-refcount.md" data-raw-source="[C28624](28624-no-release-call-to-match-incremented-refcount.md)">C28624</a></p></td>
<td align="left"><p>警告 C28624:不需要调用 release （） 以 LResultFromObject 中递增的 refcount 匹配</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28625-sensitive-data-may-be-retained.md" data-raw-source="[C28625](28625-sensitive-data-may-be-retained.md)">C28625</a></p></td>
<td align="left"><p>警告 C28625:将优化掉用于清除敏感数据的函数调用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28636-calling-localfree-on-non-allocated-pointer.md" data-raw-source="[C28636](28636-calling-localfree-on-non-allocated-pointer.md)">C28636</a></p></td>
<td align="left"><p>警告 C28636:从对 GetSecurityDescriptorOwner/组/Dacl/Sacl 的非分配指针上调用 LocalFree</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28637-calling-function-in-a-global-initializer-is-unsafe.md" data-raw-source="[C28637](28637-calling-function-in-a-global-initializer-is-unsafe.md)">C28637</a></p></td>
<td align="left"><p>警告 C28637:全局初始值设定项中调用该函数是不安全</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28638-function-delayload-stub-is-missing-declaration-.md" data-raw-source="[C28638](28638-function-delayload-stub-is-missing-declaration-.md)">C28638</a></p></td>
<td align="left"><p>警告 C28638： 函数延迟加载存根 （stub） 缺少匹配的声明</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28639-calling-close-handle-with-string.md" data-raw-source="[C28639](28639-calling-close-handle-with-string.md)">C28639</a></p></td>
<td align="left"><p>警告 C28639:使用字符串调用关闭句柄</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28640-delayload-function-stub-should-be-a-static-function.md" data-raw-source="[C28640](28640-delayload-function-stub-should-be-a-static-function.md)">C28640</a></p></td>
<td align="left"><p>警告 C28640： 函数延迟加载存根 （stub） 应为静态函数</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28644-return-value-from-dpa-insertptr-not-checked.md" data-raw-source="[C28644](28644-return-value-from-dpa-insertptr-not-checked.md)">C28644</a></p></td>
<td align="left"><p>警告 C28644:从 DPA_InsertPtr 不检查返回值</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28645-messagebox-called-using-the-question-mark-symbol.md" data-raw-source="[C28645](28645-messagebox-called-using-the-question-mark-symbol.md)">C28645</a></p></td>
<td align="left"><p>警告 C28645:使用不再建议使用问号消息符号调用了 MessageBox</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28648-pulseevent-is-an-unreliable-function.md" data-raw-source="[C28648](28648-pulseevent-is-an-unreliable-function.md)">C28648</a></p></td>
<td align="left"><p>警告 C28648:PulseEvent 是不可靠的函数</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28649-automatic-or-global-stack-arrays-are-never-null.md" data-raw-source="[C28649](28649-automatic-or-global-stack-arrays-are-never-null.md)">C28649</a></p></td>
<td align="left"><p>警告 C28649:自动或全局堆栈数组永远不会为 NULL</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28650-generic-value-is-not-treated-as-failure.md" data-raw-source="[C28650](28650-generic-value-is-not-treated-as-failure.md)">C28650</a></p></td>
<td align="left"><p>警告 C28650:要为其类型 ！ 0 是正在使用不会将它视为失败的情况。</p>
<p>如返回状态值 ！TRUE 是为返回表示失败的状态值不相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28651-member-function-pointers-cause-write-pages-copy.md" data-raw-source="[C28651](28651-member-function-pointers-cause-write-pages-copy.md)">C28651</a></p></td>
<td align="left"><p>警告 C28651:由于成员函数指针的写入页上的静态初始值设定项导致复制过程</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28652-overloaded-bitwise-operators-cause-write-pages-copy.md" data-raw-source="[C28652](28652-overloaded-bitwise-operators-cause-write-pages-copy.md)">C28652</a></p></td>
<td align="left"><p>警告 C28652:静态初始值设定项导致重载的按位运算符由于写入页上的副本</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28714-ntstatus-cast-between-semantically-different-integer-types.md" data-raw-source="[C28714](28714-ntstatus-cast-between-semantically-different-integer-types.md)">C28714</a></p></td>
<td align="left"><p>警告 C28714:语义不同的整数类型之间强制转换</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28715-boolean-cast-between-semantically-different-integer-types.md" data-raw-source="[C28715](28715-boolean-cast-between-semantically-different-integer-types.md)">C28715</a></p></td>
<td align="left"><p>警告 C28715:语义不同的整数类型之间强制转换</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28716-compiler-inserted-cast-between-semantically-different-integral.md" data-raw-source="[C28716](28716-compiler-inserted-cast-between-semantically-different-integral.md)">C28716</a></p></td>
<td align="left"><p>警告 C28716:编译器插入语义不同的整数类型之间的强制转换</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28717-invalid-variant-type.md" data-raw-source="[C28717](28717-invalid-variant-type.md)">C28717</a></p></td>
<td align="left"><p>警告 C28717:VARIANT 类型无效</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28718-unannotated-buffer.md" data-raw-source="[C28718](28718-unannotated-buffer.md)">C28718</a></p></td>
<td align="left"><p>警告 C28718:一个未批注的缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28719-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28719](28719-banned-api-usage-use-updated-function-replacement.md)">C28719</a></p></td>
<td align="left"><p>警告 C28719:已禁止的 API 用法</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28720-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28720](28720-banned-api-usage-use-updated-function-replacement.md)">C28720</a></p></td>
<td align="left"><p>警告 C28720:已禁止的 API 用法</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28721-deprecated-performance-counter-architecture.md" data-raw-source="[C28721](28721-deprecated-performance-counter-architecture.md)">C28721</a></p></td>
<td align="left"><p>警告 C28721:不推荐使用的性能计数器体系结构</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28722-unannotated-function-declaration-buffer.md" data-raw-source="[C28722](28722-unannotated-function-declaration-buffer.md)">C28722</a></p></td>
<td align="left"><p>警告 C28722:函数声明中的一个未批注的缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28723-unannotated-buffer-without-declaration.md" data-raw-source="[C28723](28723-unannotated-buffer-without-declaration.md)">C28723</a></p></td>
<td align="left"><p>警告 C28723:有没有相应的声明的函数定义中的一个未批注的缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28725-use-watson-instead.md" data-raw-source="[C28725](28725-use-watson-instead.md)">C28725</a></p></td>
<td align="left"><p>警告 C28725:而不是此 SetUnhandledExceptionFilter 使用 Watson</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28726-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28726](28726-banned-api-usage-use-updated-function-replacement.md)">C28726</a></p></td>
<td align="left"><p>警告 C28726:已禁止的 API 用法</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28727-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28727](28727-banned-api-usage-use-updated-function-replacement.md)">C28727</a></p></td>
<td align="left"><p>警告 C28727:已禁止的 API 用法</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28728-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28728](28728-banned-api-usage-use-updated-function-replacement.md)">C28728</a></p></td>
<td align="left"><p>警告 C28728:已禁止的 API 用法</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28730-possible-null-character-assignment.md" data-raw-source="[C28730](28730-possible-null-character-assignment.md)">C28730</a></p></td>
<td align="left"><p>警告 C28730:可能分配&#39;\0&#39;直接向指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28735-banned-crimson-api-usage.md" data-raw-source="[C28735](28735-banned-crimson-api-usage.md)">C28735</a></p></td>
<td align="left"><p>警告 C28735:已禁止的 Crimson API 用法</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28736-legacy-crimson-or-perflib-banned-argument-used.md" data-raw-source="[C28736](28736-legacy-crimson-or-perflib-banned-argument-used.md)">C28736</a></p></td>
<td align="left"><p>警告 C28736:已禁止的 API 参数用法</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28740-unannotated-unsigned-buffer.md" data-raw-source="[C28740](28740-unannotated-unsigned-buffer.md)">C28740</a></p></td>
<td align="left"><p>警告 C28740:一个未批注的无符号的缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28741-unannotated-non-constant-string-buffer-in-function.md" data-raw-source="[C28741](28741-unannotated-non-constant-string-buffer-in-function.md)">C28741</a></p></td>
<td align="left"><p>警告 C28741:在函数中的一个未批注的缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28742-unnanotated-non-constant-buffer-in-function.md" data-raw-source="[C28742](28742-unnanotated-non-constant-buffer-in-function.md)">C28742</a></p></td>
<td align="left"><p>警告 C28742:在函数中的一个未批注的缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28750-banned-istrlen-usage.md" data-raw-source="[C28750](28750-banned-istrlen-usage.md)">C28750</a></p></td>
<td align="left"><p>警告 C28750:已禁止的 lstrlen 及其变体的用法</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28751-banned-exallocatepool-usage.md" data-raw-source="[C28751](28751-banned-exallocatepool-usage.md)">C28751</a></p></td>
<td align="left"><p>警告 C28751:已禁止的 ExAllocatePool 及其变体的用法</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28752-banned-kernel32-advapi32-usage.md" data-raw-source="[C28752](28752-banned-kernel32-advapi32-usage.md)">C28752</a></p></td>
<td align="left"><p>警告 C28752:已禁止的 kernel32 或 advapi32 API 的用法</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28753-relying-on-undefined-order-of-evalutation-params.md" data-raw-source="[C28753](28753-relying-on-undefined-order-of-evalutation-params.md)">C28753</a></p></td>
<td align="left"><p>警告 C28753:依赖于未定义参数的计算顺序</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30029-memory-allocating-function-requests-executable-memory.md" data-raw-source="[C30029](30029-memory-allocating-function-requests-executable-memory.md)">C30029</a></p></td>
<td align="left"><p>警告 C30029:调用的内存分配请求可执行文件的内存的函数</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="30030-parameter-indicates-executable-memory.md" data-raw-source="[C30030](30030-parameter-indicates-executable-memory.md)">C30030</a></p></td>
<td align="left"><p>警告 C30030:调用内存分配函数并传递一个参数，指示可执行文件的内存</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30031-pool-n-optin-called-before-entry-function.md" data-raw-source="[C30031](30031-pool-n-optin-called-before-entry-function.md)">C30031</a></p></td>
<td align="left"><p>警告 C30031:调用内存分配函数并传递一个参数，指示可执行文件的内存</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="30032-forcing-request-of-executable-memory.md" data-raw-source="[C30032](30032-forcing-request-of-executable-memory.md)">C30032</a></p></td>
<td align="left"><p>警告 C30032:调用内存分配函数和强制执行内存使用请求<a href="https://msdn.microsoft.com/library/windows/hardware/hh920401" data-raw-source="[POOL_NX_OPTOUT](https://msdn.microsoft.com/library/windows/hardware/hh920401)">POOL_NX_OPTOUT</a>指令</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30033-executable-allocation-detected-with-pool-nx-optin.md" data-raw-source="[C30033](30033-executable-allocation-detected-with-pool-nx-optin.md)">C30033</a></p></td>
<td align="left"><p>警告 C30033:使用编译的驱动程序中，检测到可执行文件的分配<a href="https://msdn.microsoft.com/library/windows/hardware/hh920402" data-raw-source="[POOL_NX_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)">POOL_NX_OPTIN</a>。 此驱动程序已确定要在加载运行时由另一个驱动程序。 请验证是否加载驱动程序调用<strong>ExInitializeDriverRuntime (<em>DrvRtPoolNxOptIn</em>)</strong>其 DriverEntry 中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="30034-passing-flag-value-to-allocating-function.md" data-raw-source="[C30034](30034-passing-flag-value-to-allocating-function.md)">C30034</a></p></td>
<td align="left"><p>警告 C30034:传递给可能会导致可执行文件所分配的内存分配函数的标志值。 请验证正在分配的函数不请求一种形式的可执行文件的非分页缓冲池。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30035-function-call-must-be-made-inside-init-function.md" data-raw-source="[C30035](30035-function-call-must-be-made-inside-init-function.md)">C30035</a></p></td>
<td align="left"><p>警告 C30035:必须从进行初始化函数内的函数调用了 (例如， <strong>DriverEntry()</strong>或<strong>DllInitialize()</strong>)。 PREfast 无法确定是否从初始化函数进行调用。</p></td>
</tr>
</tbody>
</table>

 

 

 

