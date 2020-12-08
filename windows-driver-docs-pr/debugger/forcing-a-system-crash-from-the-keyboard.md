---
title: 通过键盘强制系统崩溃
description: 通过键盘强制系统崩溃
keywords:
- 启动进程，导致键盘系统崩溃
- CTRL + SCROLL LOCK
- 系统崩溃，由键盘导致
- bug 检查，由键盘导致
- 键盘导致系统崩溃
- USB 键盘和系统故障
- PS/2 键盘和系统故障
- 从键盘强制系统崩溃
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 75c98a559d31b904483f27d675a7bfaff084331e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838183"
---
# <a name="forcing-a-system-crash-from-the-keyboard"></a>通过键盘强制系统崩溃

## <span id="ddk_forcing_a_system_crash_from_the_keyboard_dbg"></span><span id="DDK_FORCING_A_SYSTEM_CRASH_FROM_THE_KEYBOARD_DBG"></span>

以下类型的键盘可能会直接导致系统崩溃：

<span id="________PS_2_keyboards_connected_on_i8042prt_ports_______"></span><span id="________ps_2_keyboards_connected_on_i8042prt_ports_______"></span><span id="________PS_2_KEYBOARDS_CONNECTED_ON_I8042PRT_PORTS_______"></span>**在 i8042prt 端口上连接的 PS/2 键盘**

此功能在 windows 2000 和更高版本的 Windows 操作系统中可用。

<span id="________USB_keyboards_______"></span><span id="________usb_keyboards_______"></span><span id="________USB_KEYBOARDS_______"></span>**USB 键盘**

此功能在 Windows Vista 和更高版本的 Windows 操作系统中可用。

<span id="hyper_v_keyboards_______"></span>**Hyper-v 键盘**

此功能在 windows 10 版本1903及更高版本的 Windows 操作系统中可用。

<span id="Configuration"></span> **配置**

使用键盘配置以下设置以启用系统崩溃：

1. 如果希望写入故障转储文件，则必须启用此类转储文件，选择路径和文件名，然后选择转储文件的大小。 有关详细信息，请参阅 [启用 Kernel-Mode 转储文件](enabling-a-kernel-mode-dump-file.md)。

2. 对于 PS/2 键盘，必须在注册表中启用键盘启动的故障。 在 "注册表项 **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Services \\ i8042prt \\ 参数**" 中，创建一个名为 " **CrashOnCtrlScroll**" 的值，并将其设置为等于 "0x01" 的 "REG \_ DWORD" 值。

3. 使用 USB 键盘，必须在注册表中启用键盘启动的故障。 在 "注册表项 **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Services \\ kbdhid \\ 参数** " 中，创建一个名为 " **CrashOnCtrlScroll**" 的值，并将其设置为等于 "0x01" 的 "REG \_ DWORD" 值。

4. 使用 Hyper-v 键盘，必须在注册表中启用键盘启动的故障。 在 "注册表项 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\hyperkbd\Parameters** 中，创建一个名为" **CrashOnCtrlScroll**"的值，并将其设置为等于 REG_DWORD 值0x01。

必须重新启动系统才能使这些设置生效。

完成此操作后，可以使用以下热键序列启动键盘故障：按住最右的 CTRL 键，然后按两次滚动锁定键。

然后，系统会调用 **KeBugCheck** 并发出 [**bug 检查 0xE2**](bug-check-0xe2--manually-initiated-crash.md) (手动 \_ 启动 \_ 崩溃) 。 除非已禁用故障转储，否则将在此时写入故障转储文件。

如果将内核调试器连接到崩溃的计算机，则在写入故障转储文件后，计算机将进入内核调试器。

有关使用此功能的详细信息，请参阅 [Windows 功能一文允许使用键盘生成内存转储文件](https://support.microsoft.com/help/244139/windows-feature-lets-you-generate-a-memory-dump-file-by-using-the-keyb)。

### <a name="span-iddefining_alternate_keyboard_shortcuts_to_force_a_system_crash_from_thespanspan-iddefining_alternate_keyboard_shortcuts_to_force_a_system_crash_from_thespandefining-alternate-keyboard-shortcuts-to-force-a-system-crash-from-the-keyboard"></a><span id="defining_alternate_keyboard_shortcuts_to_force_a_system_crash_from_the"></span><span id="DEFINING_ALTERNATE_KEYBOARD_SHORTCUTS_TO_FORCE_A_SYSTEM_CRASH_FROM_THE"></span>定义备用键盘快捷方式以强制从键盘系统崩溃

您可以为不同的键盘快捷键序列配置以下注册表子项下的值，以生成内存转储文件：

- 对于 PS/2 键盘：

    **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Services \\ i8042prt \\ 故障机**

- 对于 USB 键盘：

    **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Services \\ kbdhid \\ 故障机**

- 对于 Hyper-v 键盘：

    **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\hyperkbd\crashdump**

你必须 \_ 在这些子项下创建以下注册表 REG DWORD 值：

<span id="Dump1Keys"></span><span id="dump1keys"></span><span id="DUMP1KEYS"></span>**Dump1Keys**  
**Dump1Keys** 注册表值是要使用的第一个热键的位图。 例如，可以将第一个热键设置为最左侧的 SHIFT 键，而不是使用最右的 CTRL 键来启动热键序列。

下表描述了第一个热键的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">键盘快捷方式序列中使用的第一个键</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>最右边的 SHIFT 键</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>最右边的 CTRL 键</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>最右边的 ALT 键</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>最左端的 SHIFT 键</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>最左端的 CTRL 键</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x40</p></td>
<td align="left"><p>最左端的 ALT 键</p></td>
</tr>
</tbody>
</table>

**注意**  可以为 **Dump1Keys** 指定一个值，该值可启用一个或多个键作为键盘快捷键序列中使用的第一个键。 例如，将 **Dump1Keys** 的值指定为0x11，将最右边和最左端的 SHIFT 键定义为键盘快捷方式序列中的第一个键。

<span id="Dump2Key"></span><span id="dump2key"></span><span id="DUMP2KEY"></span>**Dump2Key**  
**Dump2Key** 注册表值是目标计算机的键盘布局的 scancode 表中的索引。 下面是驱动程序中的实际表。

```cpp
const UCHAR keyToScanTbl[134] = { 
        0x00,0x29,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,
        0x0A,0x0B,0x0C,0x0D,0x7D,0x0E,0x0F,0x10,0x11,0x12,
        0x13,0x14,0x15,0x16,0x17,0x18,0x19,0x1A,0x1B,0x00,
        0x3A,0x1E,0x1F,0x20,0x21,0x22,0x23,0x24,0x25,0x26,
        0x27,0x28,0x2B,0x1C,0x2A,0x00,0x2C,0x2D,0x2E,0x2F,
        0x30,0x31,0x32,0x33,0x34,0x35,0x73,0x36,0x1D,0x00,
        0x38,0x39,0xB8,0x00,0x9D,0x00,0x00,0x00,0x00,0x00,
        0x00,0x00,0x00,0x00,0x00,0xD2,0xD3,0x00,0x00,0xCB,
        0xC7,0xCF,0x00,0xC8,0xD0,0xC9,0xD1,0x00,0x00,0xCD,
        0x45,0x47,0x4B,0x4F,0x00,0xB5,0x48,0x4C,0x50,0x52,
        0x37,0x49,0x4D,0x51,0x53,0x4A,0x4E,0x00,0x9C,0x00,
        0x01,0x00,0x3B,0x3C,0x3D,0x3E,0x3F,0x40,0x41,0x42,
        0x43,0x44,0x57,0x58,0x00,0x46,0x00,0x00,0x00,0x00,
        0x00,0x7B,0x79,0x70 };
```

**注意**   124 (sysreq) 的索引是一种特殊情况，因为84键键盘具有不同的扫描代码。

如果定义备用键盘快捷方式来强制从 USB 或 PS/2 键盘进行系统崩溃，则必须将 **CrashOnCtrlScroll** 注册表值设置为0，或将其从注册表中删除。

### <a name="span-idlimitationsspanspan-idlimitationsspanlimitations"></a><span id="limitations"></span><span id="LIMITATIONS"></span>限制

系统可能会冻结，因为键盘快捷方式序列将不起作用。 但这应该非常罕见。 使用键盘快捷键序列启动崩溃即使在许多情况下，如 CTRL + ALT + DELETE 不起作用也是如此。

如果计算机在高中断请求级别上停止响应 (IRQL) ，则从键盘强制系统崩溃不起作用。 存在此限制的原因是 Kbdhid.sys 的驱动程序（该驱动程序允许内存转储进程运行）的 IRQL 低于 i8042prt.sys 驱动程序。
