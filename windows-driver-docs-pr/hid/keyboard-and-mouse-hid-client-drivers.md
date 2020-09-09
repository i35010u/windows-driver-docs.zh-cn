---
title: 键盘和鼠标 HID 客户端驱动程序
description: 键盘和鼠标 HID 客户端驱动程序。
ms.assetid: DAD50261-7619-4554-B864-9158A0FA1ACE
keywords:
- HID 键盘驱动程序
- 键盘驱动程序，HID
- 适用于 Windows 的 HID 键盘驱动程序
- HID 鼠标驱动程序
- 鼠标驱动程序，HID
- 适用于 Windows 的 HID 鼠标驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 748e1db78f96a6b682b86ba9b8d27a7bcfb49013
ms.sourcegitcommit: 9145bffd4cc3b990a9ebff43b588db6ef2001f5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89592413"
---
# <a name="keyboard-and-mouse-hid-client-drivers"></a>键盘和鼠标 HID 客户端驱动程序

> [!NOTE]
> 本主题适用于为键盘和鼠标 HID 客户端创建驱动程序的开发人员。 如果你想要修复鼠标或键盘，请参阅：
>
> - [Windows 中的鼠标、触摸板和键盘问题](https://support.microsoft.com/help/17417/windows-mouse-touchpad-keyboard-problems)
> - [排查无法正常工作的无线鼠标问题](https://support.microsoft.com/help/321122/troubleshoot-a-wireless-mouse-that-does-not-function-correctly)

本主题讨论键盘和鼠标 HID 客户端驱动程序。 键盘和鼠标表示在 HID 使用情况表中进行标准化并在 Windows 操作系统中实现的第一组 HID 客户端。

键盘和鼠标 HID 客户端驱动程序以 HID 映射器驱动程序的形式实现。 HID 映射器驱动程序是一种内核模式 WDM 筛选器驱动程序，它为非 HID 类驱动程序与 HID 类驱动程序之间的 i/o 请求提供双向接口。 映射器驱动程序将一个 i/o 请求和数据协议映射到另一个。

Windows 为 HID 键盘和 HID 鼠标设备提供系统提供的 HID 映射器驱动程序。

## <a name="architecture-and-overview"></a>体系结构和概述

下图说明了用于 USB 键盘和鼠标/触摸板设备的系统提供的驱动程序堆栈。

![键盘和鼠标驱动程序堆栈关系图，其中显示了键盘和鼠标的 hid 类映射器驱动程序以及键盘和鼠标类驱动程序。](images/keyboard-driver-stack.png)

上图包含以下组件：

- KBDHID.sys –适用于键盘的 HID 客户端映射器驱动程序。 将 HID 用法转换为 scancodes，以便与现有的键盘类驱动程序一起使用。
- MOUHID.sys-用于鼠标/触摸板的 HID 客户端映射器驱动程序。 将 HID 用法转换为鼠标命令 (X/Y、按钮、滚轮) 与现有键盘类驱动程序的接口。
- KBDCLASS.sys –键盘类驱动程序以安全的方式维护系统上所有键盘和键盘的功能。
- MOUCLASS.sys –鼠标类驱动程序在系统上维护所有鼠标/触摸板的功能。 驱动程序支持绝对和相对指针设备。 这不是 touchscreens 的驱动程序，因为它是由 Windows 中的其他驱动程序管理的。

系统生成驱动程序堆栈，如下所示：

- 传输堆栈为附加的每个 HID 设备创建一个 (PDO) 的物理设备对象，并加载相应的 HID 传输驱动程序，进而加载 HID 类驱动程序。
- HID 类驱动程序为每个键盘或鼠标 TLC 创建一个 PDO。 复杂 HID 设备 (超过1个 TLC) 将公开为 HID 类驱动程序创建的多个 PDOs。 例如，带有集成鼠标的键盘可能有一个用于标准键盘控件的集合和一个不同的鼠标集合。
- 键盘或鼠标 hid 客户端映射器驱动程序加载到相应的 FDO 上。
- HID 映射器驱动程序为键盘和鼠标创建 FDOs，并加载类驱动程序。

重要说明：

- 与受支持的 HID 用法和顶级集合兼容的键盘和鼠标不需要供应商驱动程序。
- 供应商可以选择在 HID 堆栈中提供筛选器驱动程序，以更改/增强这些特定 TLC 的功能。
- 供应商应创建单独的 TLCs （特定于供应商），以便在其 hid 客户端和设备之间交换供应商专有数据。 避免使用筛选器驱动程序，除非是关键。
- 系统打开所有键盘和鼠标集合，以独占使用。
- 系统禁止禁用/启用键盘。
- 系统为具有平滑滚动功能的水平/垂直轮提供支持。

## <a name="driver-guidance"></a>驱动程序指南

Microsoft 为 Ihv 编写驱动程序提供以下指导：

1. 允许驱动程序开发人员以筛选器驱动程序或新的 HID 客户端驱动程序的形式添加其他驱动程序。 条件如下所述：
    1. 筛选器驱动程序：驱动程序开发人员应确保其增值驱动程序是筛选器驱动程序，并且不会替换 (或用于替代输入堆栈中的) 现有 Windows HID 驱动程序。
        - 在以下情况下允许使用筛选器驱动程序：
            - 作为 kbdhid/mouhid 的上限筛选器
            - 作为 kbdclass/mouclass 的上限筛选器
        - _不_建议使用筛选器驱动程序作为 HIDCLASS 与 HID 传输微型驱动程序之间的筛选器。

    2. 函数驱动程序：或者，供应商可以创建函数驱动程序 (而不是筛选器驱动程序) 但仅针对特定于供应商的 HID PDOs (与用户模式服务如有必要) 。

        在以下情况下允许使用函数驱动程序：

        - 仅负载特定供应商的硬件

    3. 传输驱动程序： Windows 团队不建议创建其他 HID 传输微型驱动程序，因为它们是编写/维护的复杂驱动程序。 如果合作伙伴正在创建新的 HID 传输微型驱动程序，尤其是在 SoC 系统上，我们建议进行详细的体系结构审查，以了解原因并确保正确开发该驱动程序。

2. 驱动程序开发人员应利用驱动程序框架 (KMDF 或 UMDF) ，而不是依赖于 WDM 来实现其筛选器驱动程序。
3. 驱动程序开发人员应减少其服务与驱动程序堆栈之间内核用户转换的数量。
4. 驱动程序开发人员应确保能够通过键盘和触摸板功能唤醒系统 ( (设备管理器) 或 PC 制造商) 进行调整。 除了 SoC 系统外，这些设备还必须能够在系统处于正常运行的 S0 状态时将其自身从较低的状态唤醒。
5. 驱动程序开发人员应确保对其硬件进行高性能的管理。
    - 设备处于空闲状态时，设备可以进入其最低电量状态。
    - 当系统处于低功耗状态时，设备处于最低功率状态 (例如，待机 (S3) 或连接待机) 。

## <a name="keyboard-layout"></a>键盘布局

*键盘布局*充分描述了 Microsoft Windows 2000 和更高版本的键盘输入特征。 例如，键盘布局指定语言、键盘类型和版本、修饰符、扫描代码等。

有关键盘布局的信息，请参阅以下内容：

- Windows 驱动程序开发工具包中的键盘头文件 kdb (DDK) ，它记录有关键盘布局的一般信息。

- 示例键盘 [布局](https://go.microsoft.com/fwlink/p/?linkid=256128)。

若要可视化特定键盘的布局，请参阅 [Windows 键盘布局](/globalization/windows-keyboard-layouts)。

有关键盘布局的其他详细信息，请访问控制面板 \\ 时钟、语言和区域 \\ 语言。

## <a name="supported-buttons-and-wheels-on-mice"></a>鼠标上支持的按钮和轮

下表列出了不同客户端版本的 Windows 操作系统所支持的功能。

|Feature|Windows XP|Windows Vista|Windows 7|Windows 8 及更高版本|
|----|----|----|----|----|
|按钮1-5|支持 (P/2 & HID) |支持的 (PS/2 & HID) |支持的 (PS/2 & HID) |支持的 (PS/2 & HID) |
|垂直滚轮|支持的 (PS/2 & HID) |支持的 (PS/2 & HID) |支持的 (PS/2 & HID) |支持的 (PS/2 & HID) |
|水平滚轮|不支持|仅支持 (HID) |仅支持 (HID) |仅支持 (HID) |
|平滑滚动轮支持 (水平和垂直) |不支持|部分支持|仅支持 (HID) |仅支持 (HID) |

### <a name="activating-buttons-4-5-and-wheel-on-ps2-mice"></a>激活 PS/2 鼠标上的按钮4-5 和轮

Windows 用于激活新 4&5 按钮 + 滚轮模式的方法是用于在智能鼠标兼容鼠标中激活第三个按钮和滑轮的方法的扩展：

- 首先，将鼠标设置为三按钮滚轮模式，这是通过将报表速率连续设置为200报表/秒，然后将其设置为每秒100个80报表，然后从鼠标读取 ID 来完成的。 此序列完成后，鼠标应报告 ID 3。
- 接下来，将鼠标设置为5按钮滚轮模式，这是通过以下方式实现的：将报表速率连续设置为200个报表/秒，然后再次将其设置为每秒200个报表，80然后从鼠标读取该 ID。 此序列完成后，5按钮滚轮会报告 ID 为 4 (，而与智能鼠标兼容的3按钮鼠标轮鼠标仍会报告 ID 为 3) 。

请注意，这仅适用于 PS/2 鼠标，不适用于 HID 鼠标 (HID 鼠标必须在其报表描述符) 中报告准确的使用情况。

#### <a name="standard-ps2-compatible-mouse-data-packet-format-2-buttons"></a>标准 PS/2 兼容的鼠标数据数据包格式 (2 个按钮) 

|Byte|D7|D6|D5|D4|D3|D2|D1|D0|评论|
|------|-------|-------|-------|-------|-----|-----|-----|-----|-----|
| 1    | Yover | Xover | Ysign | Xsign | 标记 | M   | R   | L   | X/Y overvlows 和符号、按钮 |
| 2    | X 7    | X6    | X5    | X4    | X3  | X2  | X1  | X0  | X 数据字节                      |
| 3    | Y7    | Y6    | 是5    | Y4    | 是3  | 是2  | 是1  | Y0  | Y 数据字节数                     |

> [!NOTE]
> Windows 鼠标驱动程序不检查溢出位。 如果溢出，则鼠标只需发送最大的带符号置换值即可。

#### <a name="standard-ps2-compatible-mouse-data-packet-format-3-buttons--verticalwheel"></a>标准 PS/2 兼容的鼠标数据包格式 (3 个按钮 + VerticalWheel) 

| Byte | D7  | D6  | D5    | D4    | D3  | D2  | D1  | D0  | 评论                     |
|------|-----|-----|-------|-------|-----|-----|-----|-----|-----------------------------|
| 1    | 0   | 0   | Ysign | Xsign | 1   | M   | R   | L   | X/Y 号和 R/L/M 按钮 |
| 2    | X 7  | X6  | X5    | X4    | X3  | X2  | X1  | X0  | X 数据字节                 |
| 3    | Y7  | Y6  | 是5    | Y4    | 是3  | 是2  | 是1  | Y0  | Y 数据字节数                |
| 4    | Z7  | Z6  | Z5    | Z4    | Z3  | Z2  | Z1  | A-za-z0  | Z/滑轮数据字节           |

#### <a name="standard-ps2-compatible-mouse-data-packet-format-5-buttons--verticalwheel"></a>标准 PS/2 兼容的鼠标数据包格式 (5 个按钮 + VerticalWheel) 

| Byte | D7  | D6  | D5    | D4    | D3  | D2  | D1  | D0  | 评论                               |
|------|-----|-----|-------|-------|-----|-----|-----|-----|---------------------------------------|
| 1    | 0   | 0   | Ysign | Xsign | 1   | M   | R   | L   | X/Y 号和 R/L/M 按钮           |
| 2    | X 7  | X6  | X5    | X4    | X3  | X2  | X1  | X0  | X 数据字节                           |
| 3    | Y7  | Y6  | 是5    | Y4    | 是3  | 是2  | 是1  | Y0  | Y 数据字节数                          |
| 4    | 0   | 0   | B5    | B4    | Z3  | Z2  | Z1  | A-za-z0  | Z/滑轮数据和按钮4和5 |

>[!IMPORTANT]
>请注意，5按钮滚轮鼠标的 Z/轮数据已缩小为四位，而不是在智能鼠标兼容的三按钮滚轮模式下使用的8位。 这种减少的原因是，在任何给定的中断期间，滑轮通常不能生成超出范围 + 7/-8 的值。 当鼠标处于5按钮轮模式下时，Windows 鼠标驱动程序将对四个 Z/滑轮数据位进行签名，而当鼠标在三按钮滚轮模式下操作时，将会将整个 Z/轮数据字节扩展为。
>
>按钮 4 & 5 上的将映射到 WM \_ APPCOMMAND 消息，并对应于应用 \_ 返回和应用 \_ 转发。

### <a name="devices-not-requiring-vendor-drivers"></a>不需要供应商驱动程序的设备

以下设备不需要供应商驱动程序：

- 符合 HID 标准的设备。
- 由系统提供的非 HIDClass 驱动程序操作的键盘、鼠标或游戏端口设备。

## <a name="kbfiltr-sample"></a>Kbfiltr 示例

Kbfiltr 旨在与 Kbdclass 配合使用，这是用于键盘设备和 I8042prt 的系统类驱动程序，用于 PS/2 样式键盘的函数驱动程序。 Kbfiltr 演示如何筛选 i/o 请求，以及如何添加回调例程来修改 Kbdclass 和 I8042prt 的操作。

有关 Kbfiltr 操作的详细信息，请参阅以下内容：

- Ntddkbd WDK 标头文件。

- 示例 [Kbfiltr](https://go.microsoft.com/fwlink/p/?linkid=256125) 源代码。

### <a name="kbfiltr-ioctls"></a>Kbfiltr IOCTLs

#### <a name="ioctl_internal_i8042_hook_keyboard"></a>IOCTL_INTERNAL_I8042_HOOK_KEYBOARD

IOCTL_INTERNAL_I8042_HOOK_KEYBOARD 请求执行以下操作：

- 将初始化回调例程添加到 I8042prt 键盘初始化例程。
- 向 I8042prt 键盘 ISR 添加 ISR 回调例程。

初始化和 ISR 回调是可选的，由 PS/2 样式键盘设备的高级筛选器驱动程序提供。

I8042prt 收到 **IOCTL_INTERNAL_KEYBOARD_CONNECT** 请求后，它会将同步 **IOCTL_INTERNAL_I8042_HOOK_KEYBOARD** 请求发送到键盘设备堆栈的顶部。

Kbfiltr 接收到挂钩键盘请求后，Kbfiltr 按以下方式筛选请求：

- 保存传递给 Kbfiltr 的高级信息，其中包括高级设备对象的上下文、指向初始化回调的指针和指向 ISR 回调的指针。
- 将上层信息替换为自己的信息。
- 将 I8042prt 和指针的上下文保存到 Kbfiltr ISR 回调可以使用的回调。

#### <a name="ioctl_internal_keyboard_connect"></a>IOCTL_INTERNAL_KEYBOARD_CONNECT

**IOCTL_INTERNAL_KEYBOARD_CONNECT**请求将 Kbdclass 服务连接到键盘设备。 在打开键盘设备之前，Kbdclass 会将此请求沿键盘设备堆栈向下发送。

Kbfiltr 收到键盘连接请求后，Kbfiltr 会按以下方式筛选连接请求：

- 保存 Kbdclass 的 **CONNECT_DATA (Kbdclass) ** 结构的副本，该副本通过 Kbdclass 传递到筛选器驱动程序。
- 替换类驱动程序连接信息的自己的连接信息。
- 将 **IOCTL_INTERNAL_KEYBOARD_CONNECT** 请求向下发送设备堆栈。

如果请求失败，Kbfiltr 将完成请求并提供适当的错误状态。

Kbfiltr 为筛选服务回调例程提供一个模板，该模板可补充 **KeyboardClassServiceCallback**（Kbdclass 类服务回调例程）的操作。 筛选服务回调可以筛选从设备输入缓冲区传输到类数据队列的输入数据。

#### <a name="ioctl_internal_keyboard_disconnect"></a>IOCTL_INTERNAL_KEYBOARD_DISCONNECT

**IOCTL_INTERNAL_KEYBOARD_DISCONNECT**请求已完成，状态为 STATUS_NOT_IMPLEMENTED。 请注意，即插即用管理器可以添加或删除即插即用键盘。

对于所有其他设备控制请求，Kbfiltr 将跳过当前的 IRP 堆栈，并向下发送请求，而无需进一步处理。

### <a name="callback-routines-implemented-by-kbfiltr"></a>Kbfiltr 实现的回调例程

#### <a name="kbfilter_initializationroutine"></a>KbFilter_InitializationRoutine

请参阅 **PI8042_KEYBOARD_INITIALIZATION_ROUTINE**

如果键盘的 I8042prt 默认初始化已足够，则不需要 **KbFilter_InitializationRoutine** 。

I8042prt 在初始化键盘时 **KbFilter_InitializationRoutine** 调用。 默认键盘初始化包括下列操作：

- 重置键盘
- 设置按键率和延迟
- 将发光二极管 (LED) 

```cpp
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
*/

NTSTATUS KbFilter_InitializationRoutine(
  In  PDEVICE_OBJECT          DeviceObject,
  In  PVOID                   SynchFuncContext,
  In  PI8042_SYNCH_READ_PORT  ReadPort,
  In  PI8042_SYNCH_WRITE_PORT WritePort,
  Out PBOOLEAN                TurnTranslationOn
);
```

#### <a name="kbfilter_isrhook"></a>KbFilter_IsrHook

请参阅 **PI8042_KEYBOARD_ISR**。 如果 I8042prt 的默认操作已足够，则不需要此回调。

I8042prt 键盘 ISR 在验证中断并读取扫描代码后调用 **KbFilter_IsrHook** 。

**KbFilter_IsrHook** 以内核模式在 I8042prt 键盘的 IRQL 下运行。

```cpp
/*
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
*/

KbFilter_IsrHook KbFilter_IsrHook(
  <em>In</em>    PDEVICE_OBJECT       DeviceObject,
  <em>In</em>    PKEYBOARD_INPUT_DATA CurrentInput,
  <em>In</em>    POUTPUT_PACKET       CurrentOutput,
  <em>Inout</em> UCHAR                StatusByte,
  <em>In</em>    PUCHAR               DataByte,
  <em>Out</em>   PBOOLEAN             ContinueProcessing,
  <em>In</em>    PKEYBOARD_SCAN_STATE ScanState
);
```

#### <a name="kbfilter_servicecallback"></a>KbFilter_ServiceCallback

请参阅 **PSERVICE_CALLBACK_ROUTINE**。

函数驱动程序的 ISR 调度完成例程调用 **KbFilter_ServiceCallback**，后者随后调用 *PSERVICE_CALLBACK_ROUTINE*的键盘类驱动程序实现。 供应商可以实现筛选器服务回调来修改从设备输入缓冲区传输到类数据队列的输入数据。 例如，回调可以删除、转换或插入数据。

```cpp
/*
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
```

## <a name="moufiltr-sample"></a>Moufiltr 示例

Moufiltr 旨在与 Mouclass 一起使用、用于 Windows 2000 和更高版本的鼠标设备的系统类驱动程序，以及 I8042prt、用于 Windows 2000 和更高版本的 PS/2 样式鼠标的函数驱动程序。 Moufiltr 演示如何筛选 i/o 请求并添加回调例程来修改 Mouclass 和 I8042prt 的操作。

### <a name="moufiltr-control-codes"></a>Moufiltr 控制代码

#### <a name="ioctl_internal_i8042_hook_mouse"></a>IOCTL_INTERNAL_I8042_HOOK_MOUSE

**IOCTL_INTERNAL_I8042_HOOK_MOUSE**请求将 isr 回调例程添加到 I8042PRT 鼠标 ISR。 ISR 回调是可选的，由一级鼠标筛选器驱动程序提供。

I8042prt 收到 **IOCTL_INTERNAL_MOUSE_CONNECT** 请求后发送此请求。 I8042prt 将同步 **IOCTL_INTERNAL_I8042_HOOK_MOUSE** 请求发送到鼠标设备堆栈的顶部。

Moufiltr 收到挂钩鼠标请求后，它将按以下方式筛选请求：

- 保存传递给 Moufiltr 的高级信息，其中包括高级设备对象的上下文和指向 ISR 回调的指针。
- 将上层信息替换为自己的信息。
- 将 I8042prt 和指针的上下文保存到 Moufiltr ISR 回调可以使用的回调。

### <a name="moufiltr-callback-routines"></a>Moufiltr 回调例程

#### <a name="ioctl_internal_mouse_connect"></a>IOCTL_INTERNAL_MOUSE_CONNECT

IOCTL_INTERNAL_MOUSE_CONNECT 请求将 Mouclass 服务连接到鼠标设备。

#### <a name="ioctl_internal_mouse_disconnect"></a>IOCTL_INTERNAL_MOUSE_DISCONNECT

IOCTL_INTERNAL_MOUSE_DISCONNECT 请求由 Moufiltr 完成，其错误状态为 STATUS_NOT_IMPLEMENTED。

对于所有其他请求，Moufiltr 将跳过当前 IRP 堆栈，并向下发送请求，而无需进一步处理。

### <a name="callback-routines"></a>回调例程

#### <a name="moufilter_isrhook"></a>MouFilter_IsrHook

请参阅 **PI8042_MOUSE_ISR**。

```cpp
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
```

如果 I8042prt 的默认操作已足够，则不需要 **MouFilter_IsrHook** 回调。

I8042prt 鼠标 ISR 在验证中断后调用 **MouFilter_IsrHook** 。

若要重置鼠标，I8042prt 将经历一系列操作 substates，其中每个操作都由一个 MOUSE_RESET_SUBSTATE 枚举值标识。 有关 I8042prt 如何重置鼠标和相应的鼠标重置 substates 的详细信息，请参阅 ntdd8042 中的 MOUSE_RESET_SUBSTATE 文档。

**MouFilter_IsrHook** 以内核模式在 I8042PRT 鼠标 ISR 的 IRQL 下运行。

#### <a name="moufilter_servicecallback"></a>MouFilter_ServiceCallback

请参阅 *PSERVICE_CALLBACK_ROUTINE*

```cpp
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
```

I8042prt 的 ISR DPC 调用 MouFilter_ServiceCallback，然后调用 MouseClassServiceCallback。 可以配置筛选器服务回调来修改从设备输入缓冲区传输到类数据队列的输入数据。 例如，回调可以删除、转换或插入数据。