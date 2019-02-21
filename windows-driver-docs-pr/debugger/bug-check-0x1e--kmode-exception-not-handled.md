---
title: Bug 检查 0x1E KMODE_EXCEPTION_NOT_HANDLED
description: KMODE_EXCEPTION_NOT_HANDLED bug 检查具有 0x0000001E 值。 这表示内核模式程序生成的错误处理程序未捕获了异常。
ms.assetid: 4a30b770-b2c4-4fdd-b431-95f2b40ef5f7
keywords:
- Bug 检查 0x1E KMODE_EXCEPTION_NOT_HANDLED
- KMODE_EXCEPTION_NOT_HANDLED
ms.date: 08/23/2018
topic_type:
- apiref
api_name:
- KMODE_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b724a24b592c27e335eb4c1d64c60d2c3912b567
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525092"
---
# <a name="bug-check-0x1e-kmodeexceptionnothandled"></a>Bug 检查 0x1E:KMODE\_异常\_不\_已处理


KMODE\_异常\_不\_已处理错误检查的值为 0x0000001E。 这表示内核模式程序生成的错误处理程序未捕获了异常。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="kmodeexceptionnothandled-parameters"></a>KMODE\_异常\_不\_HANDLED 参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>未处理异常代码</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>发生了异常地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>异常的参数 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>异常的参数 1</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

这是常见 bug 检查。 若要解释它，必须标识生成的异常。

常见的异常代码包括：

-   数 0x80000002:状态\_数据类型\_未对齐

    遇到未对齐的数据引用。

-   0x80000003:状态\_断点

    没有内核调试器已附加到系统时出现断点或断言。

-   0xC0000005:状态\_访问\_冲突

    出现内存访问冲突。 （检查错误的参数 4 是驱动程序尝试访问的地址。）

异常代码的完整列表，请参阅[NTSTATUS 值](https://msdn.microsoft.com/library/cc704588.aspx)。 在 ntstatus.h 文件位于的 inc 目录中还列出了异常代码[Windows 驱动程序工具包](https://docs.microsoft.com/windows-hardware/drivers/)。


<a name="resolution"></a>分辨率
----------

**如果你不是好地调试此问题**，可以使用中所述的一些基本的故障排除技巧[**蓝色屏幕数据**](blue-screen-data.md)。 如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

**如果你打算调试该问题**，您可能会发现很难获取堆栈跟踪。 驱动程序或导致此问题的函数，则应找出参数 2 （异常地址）。

如果异常代码 0x80000003 发生，则表明已达到硬编码断点或断言，但系统已开始使用 **/NODEBUG**切换。 此问题很少发生。 如果重复发生，请确保连接到内核调试器，并且系统开始使用 **/debug**切换。

如果发生异常的代码数 0x80000002，陷阱框架将提供的其他信息。

如果特定异常的原因未知，则要考虑以下事项：

**硬件不兼容性**

确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

**有故障的设备驱动程序或系统服务**

此外，有故障的设备驱动程序或系统服务可能导致此错误。 硬件问题，例如 BIOS 不兼容性、 内存冲突和 IRQ 冲突还可以生成此错误。

如果驱动程序列出的 bug 检查消息中的名称，请禁用或删除该驱动程序。 禁用或删除任何驱动程序或最近添加的服务。 如果在启动序列期间发生错误，而且使用 NTFS 文件系统格式化的系统分区，您可以使用安全模式下禁用驱动程序在设备管理器。

检查事件查看器中的系统日志可能会帮助找出设备或驱动程序导致 bug 检查 0x1E 的其他错误消息。 您还应运行硬件诊断，尤其是内存扫描程序，系统制造商提供。 有关这些过程的详细信息，请参阅您的计算机的所有者的手册。

在 Windows 安装过程中或在安装完成后，在第一重启后可能出现此错误，将生成此消息。 错误的可能原因是系统 BIOS 不兼容性。 可以通过升级系统 BIOS 版本来解决 BIOS 问题。

**若要获取堆栈跟踪，如果普通的堆栈跟踪过程失败**

1.  使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令以显示堆栈跟踪中的参数。 查找对调用**NT ！PspUnhandledExceptionInSystemThread**。 （如果未列出此函数，请参阅下面的说明。）

2.  第一个参数**NT ！PspUnhandledExceptionInSystemThread**指向结构，其中包含指向指针的指针**除**语句：

    ```cpp
    typedef struct _EXCEPTION_POINTERS {
        PEXCEPTION_RECORD ExceptionRecord;
        PCONTEXT ContextRecord;
        } EXCEPTION_POINTERS, *PEXCEPTION_POINTERS;

    ULONG PspUnhandledExceptionInSystemThread(
        IN PEXCEPTION_POINTERS ExceptionPointers
        )
    ```

    使用[ **dd （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令以显示所需的数据该地址上。

3.  第一个检索到的值是异常记录，第二个上下文记录。 使用[ **.exr （显示异常记录）** ](-exr--display-exception-record-.md)命令并[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令为这两个值其参数，分别。

4.  之后 **.cxr**命令执行时，使用**kb**命令以显示上下文记录信息为基础的堆栈跟踪。 此堆栈跟踪指示发生未处理的异常的调用堆栈。

**请注意**  此过程假定您可以找到**NT ！PspUnhandledExceptionInSystemThread**。 但是，在某些情况下 （如访问冲突故障），将不能执行此操作。 在这种情况下，查找**ntoskrnl ！KiDispatchException**。 传递给此函数的第三个参数是一个陷阱帧地址。 使用[ **.trap （显示陷阱帧）** ](-trap--display-trap-frame-.md)命令使用此地址将注册上下文设置为适当的值。 然后可以执行堆栈跟踪，并发出其他命令。

 

下面是示例的 bug 检查 0x1E x86 处理器：

```dbgcmd
kd> .bugcheck                 get the bug check data
Bugcheck code 0000001e
Arguments c0000005 8013cd0a 00000000 0362cffff

kd> kb                        start with a stack trace 
FramePtr  RetAddr   Param1   Param2   Param3   Function Name 
8013ed5c  801263ba  00000000 00000000 fe40cb00 NT!_DbgBreakPoint 
8013eecc  8013313c  0000001e c0000005 8013cd0a NT!_KeBugCheckEx+0x194
fe40cad0  8013318e  fe40caf8 801359ff fe40cb00 NT!PspUnhandledExceptionInSystemThread+0x18
fe40cad8  801359ff  fe40cb00 00000000 fe40cb00 NT!PspSystemThreadStartup+0x4a
fe40cf7c  8013cb8e  fe43a44c ff6ce388 00000000 NT!_except_handler3+0x47
00000000  00000000  00000000 00000000 00000000 NT!KiThreadStartup+0xe

kd> dd fe40caf8 L2            dump EXCEPTION_POINTERS structure
0xFE40CAF8  fe40cd88 fe40cbc4                   ..@...@.

kd> .exr fe40cd88             first DWORD is the exception record
Exception Record @ FE40CD88:
   ExceptionCode: c0000005
  ExceptionFlags: 00000000
  Chained Record: 00000000
ExceptionAddress: 8013cd0a
NumberParameters: 00000002
   Parameter[0]: 00000000
   Parameter[1]: 0362cfff

kd> .cxr fe40cbc4             second DWORD is the context record
CtxFlags: 00010017
eax=00087000 ebx=00000000 ecx=03ff0000 edx=ff63d000 esi=0362cfff edi=036b3fff
eip=8013cd0a esp=fe40ce50 ebp=fe40cef8 iopl=0         nv dn ei pl nz ac po cy
vip=0    vif=0
cs=0008  ss=0010  ds=0023  es=0023  fs=0030  gs=0000             efl=00010617
0x8013cd0a  f3a4             rep movsb

kd> kb                        kb gives stack for context record
ChildEBP RetAddr  Args to Child
fe40ce54 80402e09 ff6c4000 ff63d000 03ff0000 NT!_RtlMoveMemory@12+0x3e
fe40ce68 80403c18 ffbc0c28 ff6ce008 ff6c4000 HAL!_HalpCopyBufferMap@20+0x49
fe40ce9c fe43b1e4 ff6cef90 ffbc0c28 ff6ce009 HAL!_IoFlushAdapterBuffers@24+0x148
fe40ceb8 fe4385b4 ff6ce388 6cd00800 ffbc0c28 QIC117!_kdi_FlushDMABuffers@20+0x28
fe40cef8 fe439894 ff6cd008 ffb6c820 fe40cf4c QIC117!_cqd_CmdReadWrite@8+0x26e
fe40cf18 fe437d92 ff6cd008 ffb6c820 ff6e4e50 QIC117!_cqd_DispatchFRB@8+0x210
fe40cf30 fe43a4f5 ff6cd008 ffb6c820 00000000 QIC117!_cqd_ProcessFRB@8+0x134
fe40cf4c 80133184 ff6ce388 00000000 00000000 QIC117!_kdi_ThreadRun@4+0xa9
fe40cf7c 8013cb8e fe43a44c ff6ce388 00000000 NT!_PspSystemThreadStartup@8+0x40
```

 

 




