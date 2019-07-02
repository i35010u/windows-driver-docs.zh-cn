---
title: 通过键盘强制系统崩溃
description: 通过键盘强制系统崩溃
ms.assetid: 0c3ec6f3-d233-46e4-b599-1a0f89318ed2
keywords:
- 启动过程中，从键盘导致系统崩溃
- CTRL + 滚动锁
- 在系统发生崩溃，导致从键盘
- 错误检查，从而导致从键盘
- 键盘导致系统崩溃
- USB 键盘和系统故障
- Ps/2 键盘和系统故障
- 从键盘强制系统崩溃
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 48279ae6fcf2cb74371abd44a4beeb41db7116fc
ms.sourcegitcommit: 2854c02cbe5b2c0010d0c64367cfe8dbd201d3f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67499805"
---
# <a name="forcing-a-system-crash-from-the-keyboard"></a>通过键盘强制系统崩溃

## <span id="ddk_forcing_a_system_crash_from_the_keyboard_dbg"></span><span id="DDK_FORCING_A_SYSTEM_CRASH_FROM_THE_KEYBOARD_DBG"></span>

以下类型的键盘可以直接导致系统崩溃：

<span id="________PS_2_keyboards_connected_on_i8042prt_ports_______"></span><span id="________ps_2_keyboards_connected_on_i8042prt_ports_______"></span><span id="________PS_2_KEYBOARDS_CONNECTED_ON_I8042PRT_PORTS_______"></span> **Ps/2 键盘 i8042prt 端口上连接**

此功能是在 Windows 2000 和更高版本的 Windows 操作系统中可用。

<span id="________USB_keyboards_______"></span><span id="________usb_keyboards_______"></span><span id="________USB_KEYBOARDS_______"></span> **USB 键盘**

此功能是在 Windows Vista 和更高版本的 Windows 操作系统中可用。

<span id="hyper_v_keyboards_______"></span> **HYPER-V 键盘**

此功能是在 Windows 10 版本 1903年和更高版本的 Windows 操作系统中可用。

<span id="Configuration"></span> **配置**

配置以下设置以启用使用键盘在系统发生崩溃：

1. 如果你想要写入的崩溃转储文件，必须启用此类转储文件，选择的路径和文件名称，然后选择转储文件的大小。 有关详细信息，请参阅[启用内核模式转储文件](enabling-a-kernel-mode-dump-file.md)。

2. 使用 ps/2 键盘，必须启用注册表中的键盘启动故障。 注册表项中**HKEY\_本地\_机\\系统\\CurrentControlSet\\Services\\i8042prt\\参数**，创建一个名为值**CrashOnCtrlScroll**，并将其设置为等于 REG\_0x01 的 DWORD 值。

3. 使用 USB 键盘，必须启用注册表中的键盘启动故障。 注册表项中**HKEY\_本地\_机\\系统\\CurrentControlSet\\Services\\kbdhid\\参数，** 创建名为值**CrashOnCtrlScroll**，并将其设置为等于 REG\_0x01 的 DWORD 值。

4. 使用 HYPER-V 键盘，必须启用注册表中的键盘启动故障。 注册表项中**HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\hyperkbd\Parameters**，创建一个名为值**CrashOnCtrlScroll**，并将其设置为等于 0x01 的 REG_DWORD 值。

必须重新启动到系统的这些设置才会生效。

完成此操作后，可以通过使用以下热键序列启动键盘故障：按下最右侧的 CTRL 键，然后按 SCROLL LOCK 键两次。

然后调用系统**KeBugCheck**和问题[ **bug 检查 0xE2** ](bug-check-0xe2--manually-initiated-crash.md) (手动\_启动\_崩溃)。 除非已禁用故障转储，此时写入崩溃转储文件。

如果内核调试程序附加到崩溃的计算机，计算机将进入内核调试器写入崩溃转储文件后。

有关使用此功能的详细信息，请参阅文章[通过使用键盘 (KB 244139) 生成内存转储文件](https://go.microsoft.com/fwlink/p/?linkid=106065)。

### <a name="span-iddefiningalternatekeyboardshortcutstoforceasystemcrashfromthespanspan-iddefiningalternatekeyboardshortcutstoforceasystemcrashfromthespandefining-alternate-keyboard-shortcuts-to-force-a-system-crash-from-the-keyboard"></a><span id="defining_alternate_keyboard_shortcuts_to_force_a_system_crash_from_the"></span><span id="DEFINING_ALTERNATE_KEYBOARD_SHORTCUTS_TO_FORCE_A_SYSTEM_CRASH_FROM_THE"></span>定义从键盘强制在系统发生崩溃的备用键盘快捷方式

你可以配置不同的键盘快捷方式序列，以生成内存转储文件的以下注册表子项中的值：

- 为 ps/2 键盘：

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\i8042prt\\crashdump**

- 有关 USB 键盘：

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\kbdhid\\crashdump**

- 有关 HYPER-V 键盘：

    **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\hyperkbd\crashdump**

必须创建以下注册表 REG\_这些子项下的 DWORD 值：

<span id="Dump1Keys"></span><span id="dump1keys"></span><span id="DUMP1KEYS"></span>**Dump1Keys**  
**Dump1Keys**注册表值是要使用的第一个热密钥的位图。 例如，而不是使用最右侧的 CTRL 键以启动热键序列，可以设置为最左侧的 SHIFT 键的第一个热键。

下表所述的第一个热键的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">使用键盘快捷方式序列中的第一个键</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>最右侧 SHIFT 键</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>最右侧的 CTRL 键</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>最右边的 ALT 键</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>最左侧 SHIFT 键</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>最左侧的 CTRL 键</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x40</p></td>
<td align="left"><p>最左侧的 ALT 键</p></td>
</tr>
</tbody>
</table>

**请注意**  可以分配**Dump1Keys**作为使用键盘快捷方式序列中的第一个密钥启用一个或多个键的值。 例如，将分配**Dump1Keys** 0x11 将定义这两个最右边和最左侧 SHIFT 键为键盘快捷方式序列中的第一个键的值。

<span id="Dump2Key"></span><span id="dump2key"></span><span id="DUMP2KEY"></span>**Dump2Key**  
**Dump2Key**注册表值是目标计算机的键盘布局的 scancode 表中的索引。 下面是驱动程序中的实际表。

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

**请注意**  索引 124 (sysreq) 是一种特殊情况，因为 84 键键盘具有不同的扫描代码。

如果定义了备用键盘快捷方式以从 USB 或 PS/2 键盘强制在系统发生崩溃，必须设置**CrashOnCtrlScroll**注册表值为 0，或将其从注册表中删除。

### <a name="span-idlimitationsspanspan-idlimitationsspanlimitations"></a><span id="limitations"></span><span id="LIMITATIONS"></span>限制

很可能要冻结的方式的键盘快捷方式序列化将不工作的系统。 但是，这应该是非常少见。 使用键盘快捷方式序列启动崩溃将适用甚至在许多情况下，CTRL + ALT + DELETE 不起作用。

从键盘强制系统崩溃不的工作原理，如果在计算机停止响应在高中断请求级别 (IRQL)。 存在此限制，因为 Kbdhid.sys 驱动程序，它允许运行的内存转储进程，在较低的 IRQL 比 i8042prt.sys 驱动程序进行操作。
