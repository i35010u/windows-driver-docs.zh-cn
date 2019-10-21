---
title: Bug 检查 0x1E KMODE_EXCEPTION_NOT_HANDLED
description: KMODE_EXCEPTION_NOT_HANDLED bug 检查的值为0x0000001E。 这表示内核模式程序生成了错误处理程序未捕获的异常。
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
ms.openlocfilehash: e203914c5659ad40f3379130173457c57834e355
ms.sourcegitcommit: 6d7f25f280af5fd4f4d9337d131c2a22288847fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359588"
---
# <a name="bug-check-0x1e-kmode_exception_not_handled"></a>Bug 检查0x1E： KMODE \_EXCEPTION \_NOT \_HANDLED


KMODE \_EXCEPTION \_NOT \_HANDLED bug 检查的值为0x0000001E。 这表示内核模式程序生成了错误处理程序未捕获的异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="kmode_exception_not_handled-parameters"></a>KMODE \_EXCEPTION \_NOT \_HANDLED 参数


<table>
<colgroup>
<col width="20%" />
<col width="80%" />
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
<td align="left"><p>未处理的异常代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>发生异常的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>异常的参数0。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>异常的参数1。</p></td>
</tr>
</tbody>
</table>


<a name="cause"></a>原因
-----

若要解释此 bug 检查，必须确定生成的异常。

常见的异常代码包括：

-   数0x80000002：状态 \_DATATYPE \_MISALIGNMENT

    遇到未对齐的数据引用。

-   0x80000003：状态 \_BREAKPOINT

    当没有内核调试器附加到系统时遇到断点或断言。

-   0xC0000005：状态 \_ACCESS \_VIOLATION

    发生了内存访问冲突。 （Bug 检查的参数4是驱动程序尝试访问的地址。）

有关异常代码的完整列表，请参阅[NTSTATUS 值](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)。 异常代码在*ntstatus*中定义，该文件是[Windows 驱动程序工具包](https://docs.microsoft.com/windows-hardware/drivers/)提供的标头文件。 （有关详细信息，请参阅[Windows 驱动程序工具包中的标头文件](../gettingstarted/header-files-in-the-windows-driver-kit.md)）。 


<a name="remarks"></a>备注
-------

如果你不打算调试此问题，则可以使用[蓝色屏幕数据](blue-screen-data.md)中所述的一些基本故障排除技术。 如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

### <a name="hardware-incompatibility"></a>硬件不兼容

确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如，可以在[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

### <a name="faulty-device-driver-or-system-service"></a>设备驱动程序或系统服务错误

此外，错误的设备驱动程序或系统服务可能会导致此错误。 硬件问题（例如 BIOS 不兼容、内存冲突和 IRQ 冲突）也可能生成此错误。

如果在 bug 检查消息中按名称列出了驱动程序，请禁用或删除该驱动程序。 禁用或删除最近添加的任何驱动程序或服务。 如果在启动序列过程中出现错误，并且使用 NTFS 文件系统格式化系统分区，则可以使用安全模式禁用设备管理器中的驱动程序。

检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致 bug 检查0x1E 的设备或驱动程序。 还应运行硬件诊断，尤其是系统制造商提供的内存扫描器。 有关这些过程的详细信息，请参阅计算机所有者手册。

在 Windows 安装程序期间或安装完成后，可能会在首次重新启动之后出现生成此消息的错误。 此错误的可能原因是系统 BIOS 不兼容。 可以通过升级系统 BIOS 版本来解决 BIOS 问题。

<a name="resolution"></a>分辨率
----------

如果打算调试此问题，您可能会发现很难获得堆栈跟踪。 异常地址（参数2）应查明导致此问题的驱动程序或函数。

异常代码0x80000003 指示命中了硬编码断点或断言，但系统是使用 **/NODEBUG**开关启动的。 此问题很少发生。 如果它反复发生，请确保已连接内核调试器，并且系统是使用 **/debug**开关启动的。

如果发生异常代码数0x80000002，陷阱帧会提供其他信息。

### <a name="unknown-cause"></a>未知原因

如果异常的特定原因未知，请考虑使用以下过程获取堆栈跟踪。

> [!NOTE]
> 此过程假定您可以找到**NT！PspUnhandledExceptionInSystemThread**。 但是，在某些情况下（如访问冲突崩溃），将无法执行此操作。 在这种情况下，请查找**ntoskrnl.exe！KiDispatchException**。 传递给此函数的第三个参数是一个陷阱帧地址。 使用带有此地址的 " [**陷阱**（显示陷印帧）](-trap--display-trap-frame-.md) " 命令可将寄存器上下文设置为合适的值。 然后，你可以执行堆栈跟踪并发出其他命令。

**如果正常堆栈跟踪过程失败，则获取堆栈跟踪**

1.  使用[ **kb** （显示 stack backtrace）](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令可在堆栈跟踪中显示参数。 查找对**NT！PspUnhandledExceptionInSystemThread**。 （如果未列出此函数，请参阅下面的说明。）

2.  NT！的第一个参数**PspUnhandledExceptionInSystemThread**是指向结构的指针，该结构包含指向**except**语句的指针：

    ```cpp
    typedef struct _EXCEPTION_POINTERS {
        PEXCEPTION_RECORD ExceptionRecord;
        PCONTEXT ContextRecord;
        } EXCEPTION_POINTERS, *PEXCEPTION_POINTERS;

    ULONG PspUnhandledExceptionInSystemThread(
        IN PEXCEPTION_POINTERS ExceptionPointers
        )
    ```

    使用该地址上的[ **dd** （显示内存）](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令显示所需数据。

3.  第一个检索到的值是异常记录，第二个值是上下文记录。 分别使用[ **.exr** （显示异常记录）](-exr--display-exception-record-.md)命令和[ **.cxr** （显示上下文记录）](-cxr--display-context-record-.md)命令，并将这两个值作为其参数。

4.  执行 **.cxr**命令后，使用**kb**命令显示基于上下文记录信息的堆栈跟踪。 此堆栈跟踪指示出现未处理异常的调用堆栈。

### <a name="example-bug-check"></a>示例 bug 检查

以下是 x86 处理器上 bug 检查0x1E 的示例：

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
