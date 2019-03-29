---
title: 键盘和鼠标 HID 客户端驱动程序
description: 键盘和鼠标 HID 客户端驱动程序。
ms.assetid: DAD50261-7619-4554-B864-9158A0FA1ACE
keywords:
- HID 的键盘驱动程序
- 键盘驱动程序，HID
- 用于 Windows 的 HID 的键盘驱动程序
- HID 的鼠标驱动程序
- 鼠标的驱动程序，HID
- 用于 Windows 的 HID 的鼠标驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4d83fcc34bcdc272e9e903ab1e9dfca6ca50893
ms.sourcegitcommit: c4dc4a78ea33537bd47fc7fb666cfd0718d302e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58349266"
---
# <a name="keyboard-and-mouse-hid-client-drivers"></a>键盘和鼠标 HID 客户端驱动程序

> [!NOTE]
> 本主题适用于开发人员创建键盘和鼠标的驱动程序 HID 客户端。 如果想要修复鼠标或键盘，请参阅：
>
> - [鼠标、 触摸板，以及在 Windows 中的键盘问题](https://support.microsoft.com/help/17417/windows-mouse-touchpad-keyboard-problems)
> - [不能正常无线鼠标进行故障排除](https://support.microsoft.com/help/321122/troubleshoot-a-wireless-mouse-that-does-not-function-correctly)

本主题讨论键盘和鼠标 HID 客户端驱动程序。 键盘和鼠标表示 HID 客户端已标准化 HID 用法表中并在 Windows 操作系统中实现的第一个集。

HID 映射器驱动程序的窗体中实现键盘和鼠标 HID 客户端驱动程序。 HID 映射器驱动程序是为非 HID 类驱动程序与 HID 类驱动程序之间的 I/O 请求提供了双向接口的内核模式 WDM 筛选器驱动程序。 映射器驱动程序将映射到另一个的 I/O 请求和数据协议。

Windows 提供 HID 键盘和鼠标 HID 设备的系统提供的 HID 映射器驱动程序。

## <a name="architecture-and-overview"></a>体系结构和概述

下图说明了 USB 键盘和鼠标/触摸板进行设备的系统提供的驱动程序堆栈。

![键盘和鼠标的驱动程序堆栈关系图，显示的 hid 的类映射器键盘和鼠标和键盘和鼠标类驱动程序的驱动程序。](images/keyboard-driver-stack.png)

上图中包括以下组件：

- KBDHID.sys – 键盘的 HID 客户端映射器驱动程序。 转换为与现有键盘类驱动程序进行交互的 scancodes HID 用法。
- MOUHID.sys – 鼠标/触摸板的 HID 客户端映射器驱动程序。 HID 用法转换为鼠标命令 (X / Y、 按钮、 滚轮) 以便与现有键盘类驱动程序。
- KBDCLASS.sys – 在键盘类驱动程序以安全的方式维护所有键盘以及系统上的小键盘的功能。
- MOUCLASS.sys – 鼠标类驱动程序维护功能所有鼠标 / 系统上的触摸板。 驱动程序支持绝对和相对指针设备。 这不是触摸屏的驱动程序，如由 Windows 中的不同驱动程序。

系统将生成驱动程序堆栈，如下所示：

- 传输堆栈的每个附加的 HID 设备创建一个物理设备对象 (PDO) 并加载相应的 HID 传输驱动程序又将 HID 类驱动程序。
- HID 类驱动程序创建每个键盘或鼠标 TLC 的 PDO。 复杂的 HID 设备 (超过 1 TLC) 创建的 HID 类驱动程序的多个 PDOs 作为公开。 例如，使用集成的鼠标键盘可能有一个这样的标准键盘控件集合和鼠标的不同集合。
- 键盘或鼠标 hid 驱动程序已加载适当 FDO 的客户端映射器。
- HID 映射器驱动程序的键盘和鼠标，创建 FDOs 并加载的类驱动程序。

重要说明：

- 供应商驱动程序不需要键盘和鼠标符合受支持的 HID 用法和顶部级别的集合。
- 供应商可能会根据需要提供 HID 堆栈 alter/增强这些特定 TLC 功能中的筛选器驱动程序。
- 供应商应创建单独 TLCs，属于特定于供应商，其 hid 客户端和设备之间的供应商专有数据交换。 避免使用筛选器驱动程序，除非关键。
- 系统会打开供其独占使用的所有键盘和鼠标集合。
- 系统会阻止禁用/启用键盘。
- 系统为水平/垂直滚轮平滑滚动功能提供支持。

## <a name="driver-guidance"></a>驱动程序指南

Microsoft 提供了以下指南 ihv 编写驱动程序：

1. 驱动程序开发人员可以在筛选器驱动程序或新的 HID 客户端驱动程序的窗体中添加其他驱动程序。 条件如下所述：
    1. 筛选器驱动程序：驱动程序开发人员应确保其值添加驱动程序筛选器驱动程序，不会替换 （或） 用来代替现有的 Windows HID 驱动程序中输入的堆栈。
        - 筛选器驱动程序可以用在以下方案：
            - 作为到 kbdhid/mouhid 的上部筛选器
            - 作为到 kbdclass/mouclass 的上部筛选器
        - 筛选器驱动程序_不_建议将其作为 HIDCLASS 和 HID 传输微型驱动程序之间的筛选器

    2. 功能的驱动程序：或者供应商可以创建功能驱动程序 （而不是筛选器驱动程序） 但仅针对供应商特定的 HID PDOs （与用户模式服务如有必要）。

        功能的驱动程序可以用在以下方案：

        - 仅限特定供应商的硬件上的负载

    3. 传输驱动程序：Windows 团队不建议创建其他 HID 传输微型驱动程序，因为它们是复杂的驱动程序，以写入或维护。 如果合作伙伴已创建新 HID 传输微型驱动程序，尤其是在 SoC 系统上，我们建议详细体系结构检查，以了解原因，并确保正确开发驱动程序。

2. 驱动程序开发人员应将驱动程序框架 （KMDF 或 UMDF），并为其筛选器驱动程序依赖于 WDM。
3. 驱动程序开发人员应减少内核用户其服务和驱动程序堆栈之间的转换数。
4. 驱动程序开发人员应确保您能够通过键盘和触摸板的功能 （可由最终用户 （设备管理器） 或 PC 制造商调整） 将系统唤醒。 此外在 SoC 系统中，这些设备必须能够唤醒本身从较低功率状态，当系统处于工作 S0 状态。
5. 驱动程序开发人员应确保其硬件是电源有效地管理。
    - 当设备处于空闲状态时，设备可以转到其最小的电源状态。
    - 当系统处于低功耗状态 （例如，待机状态 (S3) 或连接的待机） 时，设备是最低的电源状态。

## <a name="keyboard-layout"></a>键盘布局

一个*键盘布局*完全键盘输入的特性进行 Microsoft Windows 2000 和更高版本进行了说明。 例如，一种键盘布局指定语言、 键盘类型和版本、 修饰符、 扫描代码等。

请参阅以下有关键盘布局的信息：

- 键盘标头文件，kdb.h，在 Windows 驱动程序开发工具包 (DDK)，用于记录有关键盘布局的常规信息。

- 示例键盘[布局](https://go.microsoft.com/fwlink/p/?linkid=256128)。

若要可视化的特定键盘布局，请参阅[Windows 键盘布局](https://docs.microsoft.com/globalization/windows-keyboard-layouts)。

有关键盘布局周围的其他详细信息，请访问控制面板\\时钟、 语言和区域\\语言。

## <a name="supported-buttons-and-wheels-on-mice"></a>受支持的按钮和在鼠标滚轮

下表标识了跨不同的客户端版本的 Windows 操作系统支持的功能。

| 功能                                               | Windows XP             | Windows Vista          | Windows 7              | Windows 8 和更高版本    |
|-------------------------------------------------------|------------------------|------------------------|------------------------|------------------------|
| 1-5 的按钮                                           | 支持 (P/2 & HID)  | 支持 (PS/2 & HID) | 支持 (PS/2 & HID) | 支持 (PS/2 & HID) |
| 垂直滚动滚轮                                 | 支持 (PS/2 & HID) | 支持 (PS/2 & HID) | 支持 (PS/2 & HID) | 支持 (PS/2 & HID) |
| 水平滚动滚轮                               | 不支持          | 支持 (HID 仅)    | 支持 (HID 仅)    | 支持 (HID 仅)    |
| 平滑滚动滚轮支持 （水平和垂直） | 不支持          | 部分支持       | 支持 (HID 仅)   | 支持 (HID 仅)   |

### <a name="activating-buttons-4-5-and-wheel-on-ps2-mice"></a>激活按钮 4-5 和在 ps/2 鼠标滚轮

Windows 用来激活新 4 和 5 按钮 + 滚轮模式的方法是方法的用来激活第三个按钮和在智能鼠标兼容鼠标滚轮的扩展：

- 首先，鼠标设置为三个按钮滚轮模式，这一点通过设置报表速率连续到 200 个报表/秒，然后为 100 秒报告，则对 80 报表/第二、，然后读取来自鼠标 ID。 此序列完成时，鼠标应报告的 ID 为 3。
- 接下来，鼠标设置为 5 按钮滚轮模式，从而通过设置报表速率连续到 200 个报表/秒，然后为 200 每秒报告再次，则为 80 报表/第二、，然后读取来自鼠标 ID。 此序列完成后，第 5 步按钮滚轮鼠标应报告的 ID 为 4 （而智能鼠标兼容 3 按钮滚轮鼠标仍会报告 ID 为 3）。

请注意这是适用于仅 ps/2 鼠标并不是适用于 HID 鼠标 （HID 鼠标必须报告其报表描述符中的准确用法）。

#### <a name="standard-ps2-compatible-mouse-data-packet-format-2-buttons"></a>标准 PS/2-兼容鼠标数据数据包的格式 （两个按钮）

| Byte | D7    | D6    | D5    | D4    | D3  | D2  | D1  | D0  | 备注                          |
|------|-------|-------|-------|-------|-----|-----|-----|-----|----------------------------------|
| 1    | Yover | 交叉 | Ysign | Xsign | Tag | M   | R   | L   | X / Y overvlows 和符号、 按钮 |
| 2    | X7    | X6    | X5    | X4    | X3  | X2  | X1  | X0  | X 数据字节                      |
| 3    | Y7    | Y6    | Y5    | Y4    | Y3  | Y2  | Y1  | Y0  | Y 数据字节数                     |

> [!NOTE]
> Windows 鼠标驱动程序不会检查溢出位。 发生溢出时，鼠标应只需发送的最大带符号的偏移量值。

#### <a name="standard-ps2-compatible-mouse-data-packet-format-3-buttons--verticalwheel"></a>标准 PS/2-兼容鼠标数据数据包的格式 （三个按钮 + VerticalWheel）

| Byte | D7  | D6  | D5    | D4    | D3  | D2  | D1  | D0  | 备注                     |
|------|-----|-----|-------|-------|-----|-----|-----|-----|-----------------------------|
| 1    | 0   | 0   | Ysign | Xsign | 1   | M   | R   | L   | X / Y 符号和 R / L / M 按钮 |
| 2    | X7  | X6  | X5    | X4    | X3  | X2  | X1  | X0  | X 数据字节                 |
| 3    | Y7  | Y6  | Y5    | Y4    | Y3  | Y2  | Y1  | Y0  | Y 数据字节数                |
| 4    | Z7  | Z6  | Z5    | Z4    | Z3  | Z2  | Z1  | Z0  | Z/滚轮数据字节           |

#### <a name="standard-ps2-compatible-mouse-data-packet-format-5-buttons--verticalwheel"></a>标准 PS/2-兼容鼠标数据数据包的格式 （5 个按钮 + VerticalWheel）

| Byte | D7  | D6  | D5    | D4    | D3  | D2  | D1  | D0  | 备注                               |
|------|-----|-----|-------|-------|-----|-----|-----|-----|---------------------------------------|
| 1    | 0   | 0   | Ysign | Xsign | 1   | M   | R   | L   | X / Y 符号和 R / L / M 按钮           |
| 2    | X7  | X6  | X5    | X4    | X3  | X2  | X1  | X0  | X 数据字节                           |
| 3    | Y7  | Y6  | Y5    | Y4    | Y3  | Y2  | Y1  | Y0  | Y 数据字节数                          |
| 4    | 0   | 0   | B5    | B4    | Z3  | Z2  | Z1  | Z0  | Z/滚轮数据和按钮 4 和 5 |

重要说明：

- 请注意到四位而不是在智能鼠标兼容 3 按钮滚轮模式下所使用的 8 位减少了 5 按钮滚轮鼠标的滚轮 Z/数据。 这种减少是通过实现这一事实，滚轮通常不能生成超出范围 + 7 /-8 的值在任何给定的中断期间。 当鼠标以在三个按钮滚轮模式下操作时，鼠标位于中第 5 步按钮滚轮模式和完整的 Z/滚轮数据字节时，驱动程序会对进行签名的 Windows 鼠标扩展四个 Z/滚轮数据位。
- 4 和 5，在按钮映射到 WM\_APPCOMMAND 消息，并对应于应用程序\_上一页和应用\_转发。

### <a name="devices-not-requiring-vendor-drivers"></a>不需要供应商驱动程序的设备

供应商驱动程序不需要的以下设备：

- 符合 HID 标准的设备。
- 键盘、 鼠标或游戏端口设备由系统提供非-HIDClass 驱动程序操作。

## <a name="kbfiltr-sample"></a>Kbfiltr 示例

Kbfiltr 旨在与 Kbdclass，键盘设备和 I8042prt，PS/2 式键盘功能驱动程序的系统类驱动程序一起使用。 Kbfiltr 演示如何筛选输入/输出请求以及如何添加更改的 Kbdclass 和 I8042prt 操作的回调例程。

有关 Kbfiltr 操作的详细信息，请参阅：

- Ntddkbd.h WDK 标头文件。

- 该示例[Kbfiltr](https://go.microsoft.com/fwlink/p/?linkid=256125)源代码。

### <a name="kbfiltr-ioctls"></a>Kbfiltr Ioctl

<table>
<tr>
<th>控制代码</th>
<th>描述</th>
</tr>
<tr>
<td>
<p>
&lt;MSHelp:link tabindex ="0"keywords="hid.ioctl_internal_i8042_hook_keyboard"&gt;<b>IOCTL_INTERNAL_I8042_HOOK_KEYBOARD</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_I8042_HOOK_KEYBOARD 请求执行以下任务：</p>
<ul>
<li>
<p>初始化回调例程向 I8042prt 键盘初始化例程</p>
</li>
<li>
<p>向 I8042prt 键盘 ISR ISR 回调例程</p>
</li>
</ul>
<p>初始化和 ISR 回调是可选的是由较高级别筛选器驱动程序为了提供 PS/2 式键盘设备。</p>
<p>I8042prt 收到后&lt;MSHelp:link tabindex ="0"keywords="hid.ioctl_internal_keyboard_connect2"&gt;<b>IOCTL_INTERNAL_KEYBOARD_CONNECT</b>&lt;/MSHelp:link&gt;请求，它将同步 IOCTL_INTERNAL_I8042_HOOK_KEYBOARD 请求发送到键盘设备堆栈的顶部。</p>
<p>Kbfiltr 收到挂钩键盘请求后，Kbfiltr 筛选请求如下所示：</p>
<ul>
<li>
<p>将保存传递给 Kbfiltr，其中包括的较高级别设备对象，初始化回调指针和指向 ISR 回调的上下文的较高级别信息</p>
</li>
<li>
<p>使用其自己替换较高级别信息</p>
</li>
<li>
<p>可以使用 Kbfiltr ISR 回调的回调到保存 I8042prt 和指针的上下文</p>
</li>
</ul>
</p>
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>
&lt;MSHelp:link tabindex ="0"keywords="hid.ioctl_internal_keyboard_connect"&gt;<b>IOCTL_INTERNAL_KEYBOARD_CONNECT</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_KEYBOARD_CONNECT 请求将 Kbdclass 服务连接到键盘设备。 打开键盘设备之前，Kbdclass 将键盘设备堆栈的下层此请求发送。 </p>
<p>Kbfiltr 接收到键盘连接请求后，Kbfiltr 筛选的连接请求如下所示：</p>
<ul>
<li>
<p>将保存 Kbdclass 的一份&lt;MSHelp:link tabindex ="0"keywords="hid.connect_data__kbdclass_"&gt;<b>CONNECT_DATA (Kbdclass)</b>&lt;/MSHelp:link&gt;传递的结构到 Kbdclass 筛选器驱动程序</p>
</li>
<li>
<p>将替换为自己的类驱动程序连接信息连接信息</p>
</li>
<li>
<p>发送设备堆栈的下层 IOCTL_INTERNAL_KEYBOARD_CONNECT 请求</p>
</li>
</ul>
<p>如果请求未成功，Kbfiltr 完成时具有相应的错误状态的请求。</p>
<p>Kbfiltr 提供的模板可以补充的操作的筛选器服务回调例程&lt;MSHelp:link tabindex ="0"keywords="hid.keyboardclassservicecallback"&gt;<b>KeyboardClassServiceCallback</b> &lt;/MSHelp:link&gt;，Kbdclass 类服务的回调例程。 筛选器服务回调可以筛选从设备输入缓冲区传输到类数据队列的输入的数据。 </p>
<dl>
<dd>
</p>
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>
&lt;MSHelp:link tabindex ="0"keywords="hid.ioctl_internal_keyboard_disconnect"&gt;<b>IOCTL_INTERNAL_KEYBOARD_DISCONNECT</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_KEYBOARD_DISCONNECT 请求状态为 STATUS_NOT_IMPLEMENTED 完成。 请注意，可以添加或删除由插 manager 插键盘。</p>
</td>
</tr>
</table>

<p>对于所有其他设备控制请求，Kbfiltr 跳过当前的 IRP 堆栈，并将设备堆栈的下层请求发送而无需进一步处理。</p>
<p><b>由 Kbfiltr 实现的回调例程</b></p>
<p>
<ul>
<li><b>KbFilter_InitializationRoutine</b>

     (see &lt;MSHelp:link tabindex="0" keywords="hid.pi8042_keyboard_initialization_routine"&gt;<b>PI8042_KEYBOARD_INITIALIZATION_ROUTINE</b>&lt;/MSHelp:link&gt;)<p><b>
          KbFilter_InitializationRoutine</b> is not needed if I8042prt's default initialization of a keyboard is sufficient.</p>
<p>I8042prt 调用<b>KbFilter_InitializationRoutine</b>当它初始化键盘。 默认键盘初始化包括以下操作： 重置键盘，设置字符重复速率和延迟时间，以及设置发光二极管 (LED)。
<pre><code>
/*
Parameters
DeviceObject [in]
Pointer to the device object that is the context for this callback.

SynchFuncContext [in]
Pointer to the context for the routines pointed to by ReadPort and Writeport.

ReadPort [in]
Pointer to the system-supplied PI8042_SYNCH_READ_PORT callback that reads from the port.

WritePort [in]
Pointer to the system-supplied PI8042_SYNCH_WRITE_PORT callback that writes to the port.

TurnTranslationOn [out]
Specifies, if TRUE, to turn translation on. Otherwise, translation is turned off.

Return value
KbFilter_InitializationRoutine returns an appropriate NTSTATUS code.

<em>/

NTSTATUS KbFilter_InitializationRoutine(
  <em>In</em>  PDEVICE_OBJECT          DeviceObject,
  <em>In</em>  PVOID                   SynchFuncContext,
  <em>In</em>  PI8042_SYNCH_READ_PORT  ReadPort,
  <em>In</em>  PI8042_SYNCH_WRITE_PORT WritePort,
  <em>Out</em> PBOOLEAN                TurnTranslationOn
);
</code></pre>
</p>
</li>
<li><b>KbFilter_IsrHook</b>

     (see &lt;MSHelp:link tabindex="0" keywords="hid.pi8042_keyboard_isr"&gt;<i>PI8042_KEYBOARD_ISR</i>&lt;/MSHelp:link&gt;)<p>This callback is not needed if the default operation of I8042prt is sufficient.</p>
<p>调用 I8042prt 键盘 ISR <b>KbFilter_IsrHook</b>之后其验证中断并读取的扫描代码。 </p>
<p><b>KbFilter_IsrHook</b>在 I8042prt 键盘 ISR.的 IRQL 在内核模式下运行</p>
<pre><code>
/</em>
Parameters
DeviceObject [in]
Pointer to the filter device object of the driver that supplies this callback.

CurrentInput [in]
Pointer to the input KEYBOARD_INPUT_DATA structure that is being constructed by the ISR.

CurrentOutput [in]
Pointer to an OUTPUT_PACKET structure that specifies the bytes that are being written to the hardware device.

StatusByte [in, out]
Specifies the status byte that is read from I/O port 60 when an interrupt occurs.

DataByte [in]
Specifies the data byte that is read from I/O port 64 when an interrupt occurs.

ContinueProcessing [out]
Specifies, if TRUE, to continue processing in the I8042prt keyboard ISR after this callback returns; otherwise, processing is not continued.

ScanState [in]
Pointer to a KEYBOARD_SCAN_STATE structure that specifies the keyboard scan state.

Return value
KbFilter_IsrHook returns TRUE if the interrupt service routine should continue; otherwise it returns FALSE.

<em>/

KbFilter_IsrHook KbFilter_IsrHook(
  <em>In</em>    PDEVICE_OBJECT       DeviceObject,
  <em>In</em>    PKEYBOARD_INPUT_DATA CurrentInput,
  <em>In</em>    POUTPUT_PACKET       CurrentOutput,
  <em>Inout</em> UCHAR                StatusByte,
  <em>In</em>    PUCHAR               DataByte,
  <em>Out</em>   PBOOLEAN             ContinueProcessing,
  <em>In</em>    PKEYBOARD_SCAN_STATE ScanState
);

);
</code></pre>
</li>
<li><b>KbFilter_ServiceCallback</b> (请参阅&lt;MSHelp:link tabindex ="0"keywords="hid.kbdclass_class_service_callback_routine"&gt;<i>PSERVICE_CALLBACK_ROUTINE</i>&lt;/MSHelp:链接&gt;)<p>该函数将驱动程序调用 ISR 调度完成例程<b>KbFilter_ServiceCallback</b>，后者随后调用在键盘类驱动程序的实现的&lt;MSHelp:link tabindex ="0"keywords="hid.kbdclass_class_service_callback_routine"&gt;<i>PSERVICE_CALLBACK_ROUTINE</i>&lt;/MSHelp:link&gt;。 供应商可以实现一个筛选器服务回调，以修改从设备的输入缓冲区传输到类数据队列的输入的数据。 例如，该回调可以删除、 转换或插入数据。
<pre><code>
/</em>
Parameters
DeviceObject [in]
Pointer to the class device object.

InputDataStart [in]
Pointer to the first keyboard input data packet in the input data buffer of the port device.

InputDataEnd [in]
Pointer to the keyboard input data packet that immediately follows the last data packet in the input data buffer of the port device.

InputDataConsumed [in, out]
Pointer to the number of keyboard input data packets that are transferred by the routine.

Return value
None

*/

VOID KbFilter_ServiceCallback(
  <em>In</em>    PDEVICE_OBJECT       DeviceObject,
  <em>In</em>    PKEYBOARD_INPUT_DATA InputDataStart,
  <em>In</em>    PKEYBOARD_INPUT_DATA InputDataEnd,
  <em>Inout</em> PULONG               InputDataConsumed
);

);
</code></pre>
</p>

## <a name="moufiltr-sample"></a>Moufiltr 示例

Moufiltr 旨在与 Mouclass，与 Windows 2000 和更高版本和 I8042prt，PS/2-样式鼠标使用 Windows 2000 和更高版本的功能驱动程序一起使用的鼠标设备的系统类驱动程序一起使用。 Moufiltr 演示了如何筛选 I/O 请求并添加更改的 Mouclass 和 I8042prt 操作的回调例程。

<table>
<tr>
<th>控制代码</th>
<th>描述</th>
</tr>
<tr>
<td>
<p>
&lt;MSHelp:link tabindex ="0"keywords="hid.ioctl_internal_i8042_hook_mouse"&gt;<b>IOCTL_INTERNAL_I8042_HOOK_MOUSE</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_I8042_HOOK_MOUSE 请求添加到 I8042prt 鼠标 ISR.ISR 回调例程 ISR 回调是可选的提供由较高级别鼠标筛选器驱动程序。</p>
<p>I8042prt 发送此请求后收到&lt;MSHelp:link tabindex ="0"keywords="hid.ioctl_internal_mouse_connect2"&gt;<b>IOCTL_INTERNAL_MOUSE_CONNECT</b>&lt;/MSHelp:link&gt;请求。 I8042prt 将同步 IOCTL_INTERNAL_I8042_HOOK_MOUSE 请求发送到鼠标设备堆栈的顶部。</p>
<p>Moufiltr 收到挂钩鼠标请求后，它将筛选请求，如下所示：</p>
<ul>
<li>
<p>将保存传递给 Moufiltr，其中包括较高级别设备对象和一个指向 ISR 回调的上下文的较高级别信息</p>
</li>
<li>
<p>使用其自己替换较高级别信息</p>
</li>
<li>
<p>可以使用 Moufiltr ISR 回调的回调到保存 I8042prt 和指针的上下文</p>
</li>
</ul>
<p>有关此请求和回调的详细信息，请参阅以下主题：</p>
<dl>
<dd>
<p>
&lt;MSHelp:link tabindex ="0"keywords="hid.i8042prt_callback_routines"&gt;I8042prt 回调例程&lt;/MSHelp:link&gt;
</p>
</dd>
<dd>
<p>
&lt;MSHelp:link tabindex ="0"keywords="hid.moufiltr_callback_routines"&gt;Moufiltr 回调例程&lt;/MSHelp:link&gt;
</p>
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>
&lt;MSHelp:link tabindex ="0"keywords="hid.ioctl_internal_mouse_connect"&gt;<b>IOCTL_INTERNAL_MOUSE_CONNECT</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_MOUSE_CONNECT 请求 Mouclass 服务连接到鼠标设备。</p>
</td>
</tr>
<tr>
<td>
<p>
&lt;MSHelp:link tabindex ="0"keywords="hid.ioctl_internal_mouse_disconnect"&gt;<b>IOCTL_INTERNAL_MOUSE_DISCONNECT</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_MOUSE_DISCONNECT 请求会结束 Moufiltr 具有 STATUS_NOT_IMPLEMENTED 的错误状态。</p>
</td>
</tr>
</table>
<p> </p>
</p>
<p>对于所有其他请求，Moufiltr 跳过当前的 IRP 堆栈，并将设备堆栈的下层请求发送而无需进一步处理。</p>
<p><b>由 Kbfiltr 实现的回调例程</b></p>
<dl>
<dd><b>MouFilter_IsrHook</b> (请参阅&lt;MSHelp:link tabindex ="0"keywords="hid.pi8042_mouse_isr"&gt;<i>PI8042_MOUSE_ISR</i>&lt;/MSHelp:link&gt;)<p>
<pre><code>
/*
Parameters
DeviceObject
Pointer to the filter device object of the driver that supplies this callback.

CurrentInput
Pointer to the input MOUSE_INPUT_DATA structure being constructed by the ISR.

CurrentOutput
Pointer to the OUTPUT_PACKET structure that specifies the bytes being written to the hardware device.

StatusByte
Specifies a status byte that is read from I/O port 60 when the interrupt occurs.

DataByte
Specifies a data byte that is read from I/O port 64 when the interrupt occurs.

ContinueProcessing
Specifies, if TRUE, that the I8042prt mouse ISR continues processing after this callback returns. Otherwise, processing is not continued.

MouseState
Pointer to a MOUSE_STATE enumeration value, which identifies the state of mouse input.

ResetSubState
Pointer to MOUSE_RESET_SUBSTATE enumeration value, which identifies the mouse reset substate. See the Remarks section.

Return value
MouFilter_IsrHook returns TRUE if the interrupt service routine should continue; otherwise it returns FALSE.

*/

BOOLEAN MouFilter_IsrHook(
   PDEVICE_OBJECT        DeviceObject,
   PMOUSE_INPUT_DATA     CurrentInput,
   POUTPUT_PACKET        CurrentOutput,
   UCHAR                 StatusByte,
   PUCHAR                DataByte,
   PBOOLEAN              ContinueProcessing,
   PMOUSE_STATE          MouseState,
   PMOUSE_RESET_SUBSTATE ResetSubState
);
</code></pre>
</p>
<p>一个<b>MouFilter_IsrHook</b>如果 I8042prt 的默认操作是足够，则不需要回调。

调用 I8042prt 鼠标 ISR <b>MouFilter_IsrHook</b>验证中断后。

若要重置鼠标，I8042prt 介绍一系列操作子状态的状态，其中每个由 MOUSE_RESET_SUBSTATE 枚举值。 详细了解如何 I8042prt 重置鼠标和相应的鼠标重置子状态的状态，请参阅中 ntdd8042.h MOUSE_RESET_SUBSTATE 的文档。

<b>MouFilter_IsrHook</b>在 I8042prt 鼠标 ISR.的 IRQL 在内核模式下运行

</p>
</dd>
<dd><b>MouFilter_ServiceCallback</b> (请参阅&lt;MSHelp:link tabindex ="0"keywords="hid.kbdclass_class_service_callback_routine"&gt;<i>PSERVICE_CALLBACK_ROUTINE</i>&lt;/MSHelp： 链接&gt;)<p>
<pre><code>
/*
Parameters
DeviceObject [in]
Pointer to the class device object.

InputDataStart [in]
Pointer to the first mouse input data packet in the input data buffer of the port device.

InputDataEnd [in]
Pointer to the mouse input data packet immediately following the last data packet in the port device's input data buffer.

InputDataConsumed [in, out]
Pointer to the number of mouse input data packets that are transferred by the routine.

Return value
None

*/

VOID MouFilter_ServiceCallback(
  _In_    PDEVICE_OBJECT    DeviceObject,
  _In_    PMOUSE_INPUT_DATA InputDataStart,
  _In_    PMOUSE_INPUT_DATA InputDataEnd,
  _Inout_ PULONG            InputDataConsumed
);
</code></pre>
</p>
<p>I8042prt ISR DPC 调用 MouFilter_ServiceCallback，后者随后调用 MouseClassServiceCallback。 若要修改的输入的数据，从设备的输入缓冲区传输到类数据队列，可以配置筛选器服务回调。 例如，该回调可以删除、 转换或插入数据。

</p>
