---
title: pci-e
description: Pci 扩展显示外围组件互连 (PCI) 总线以及连接到这些总线的任何设备的当前状态。
keywords:
- PCI 总线
- PCI 设备
- PCI 配置空间
- pci Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pci
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 539bbcd0cce4a0030ef1ae6ecc1a3bff967f543c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792033"
---
# <a name="pci"></a>!pci


**！ Pci** 扩展显示外围组件互连 (pci) 总线以及连接到这些总线的任何设备的当前状态。

```dbgcmd
!pci [Flags [Segment] [Bus [Device [Function [MinAddress MaxAddress]]]]]
```

## <a name="span-idddk__pci_dbgspanspan-idddk__pci_dbgspanparameters"></a><span id="ddk__pci_dbg"></span><span id="DDK__PCI_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定输出级别。 可以是以下位的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
导致详细显示。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
使显示包括范围从总线 0 (零) 到指定 *总线* 的所有总线。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
使显示包含原始字节格式的信息。 如果设置了 *MinAddress*、 *MaxAddress* 或标志位0x8，则也会自动设置此位。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
使显示包含原始 DWORD 格式的信息。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
使显示包含无效的设备号。 如果指定了 *Device* ，则忽略此标志。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>第 5 (0x20)   
使显示包含无效的功能号。

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>第 6 (0x40)   
使显示包含功能。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>第7位 (0x80)   
使显示器包含 Intel 8086 设备特定的信息。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)   
使显示包含 PCI 配置空间。

<span id="Bit_9__0x200_"></span><span id="bit_9__0x200_"></span><span id="BIT_9__0X200_"></span>第 9 (0x200)   
使显示内容包括段信息。 如果包含此位，则必须包含 *Segment* 参数。

<span id="Bit_10__0x400_"></span><span id="bit_10__0x400_"></span><span id="BIT_10__0X400_"></span>位 10 (0x400)   
使显示包括从段0到指定段的范围内的所有有效段。 如果包含此位，则必须包含 *Segment* 参数。

<span id="_______Segment______"></span><span id="_______segment______"></span><span id="_______SEGMENT______"></span>*段*   
指定要显示的段的编号。 段编号的范围为0到0xFFFF。 如果省略 *段* ，则显示有关主要段 (段 0) 的信息。 如果 *标志* 包含位 10 (0x400) ， *段* 指定要显示的最高有效段。

<span id="_______Bus______"></span><span id="_______bus______"></span><span id="_______BUS______"></span>*总线*   
指定要显示的总线。 *总线* 的范围为0到0xff。 如果省略此方法，则显示有关主总线 (总线 0) 的信息。 如果 *标志* 包含第1位 (0x2) ，则 *总线* 指定要显示的最高总线编号。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span>*设备*   
指定设备的槽设备号。 如果省略此内容，则打印有关所有设备的信息。

<span id="_______Function______"></span><span id="_______function______"></span><span id="_______FUNCTION______"></span>*函数*   
指定设备的槽功能号。 如果省略此内容，则打印所有设备功能的所有相关信息。

<span id="_______MinAddress______"></span><span id="_______minaddress______"></span><span id="_______MINADDRESS______"></span>*MinAddress*   
指定要从中显示原始字节或 Dword 的第一个地址。 该值必须介于0和0xFF 之间。

<span id="_______MaxAddress______"></span><span id="_______maxaddress______"></span><span id="_______MAXADDRESS______"></span>*MaxAddress*   
指定要从中显示原始字节或 Dword 的最后一个地址。 该值必须介于0和0xFF 之间，并且不能小于 *MinAddress*。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kext.dll Kdextx86.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>



此扩展命令只能与基于 x86 的目标计算机一起使用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) 此扩展命令的应用程序和其他示例。 有关 PCI 总线的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

<a name="remarks"></a>备注
-------

若要编辑 PCI 配置空间，请使用 [**！ ecb**](-ecb---ecd---ecw.md)、 **！ ecd** 或 **！ ecw**。

下面的示例显示了所有总线及其设备的列表。 执行此命令需要较长时间。 调试器扫描 PCI 总线的目标系统时，显示底部会显示一个移动计数器：

```dbgcmd
kd> !pci 2 ff
PCI Bus 0
00:0  8086:1237.02  Cmd[0106:.mb..s]  Sts[2280:.....]  Device  Host bridge
0d:0  8086:7000.01  Cmd[0007:imb...]  Sts[0280:.....]  Device  ISA bridge
0d:1  8086:7010.00  Cmd[0005:i.b...]  Sts[0280:.....]  Device  IDE controller
0e:0  1011:0021.02  Cmd[0107:imb..s]  Sts[0280:.....]  PciBridge 0->1-1  PCI-PCI bridge
10:0  102b:0519.01  Cmd[0083:im....]  Sts[0280:.....]  Device  VGA compatible controller
PCI Bus 1
08:0  10b7:9050.00  Cmd[0107:imb..s]  Sts[0200:.....]  Device  Ethernet
09:0  9004:8178.00  Cmd[0117:imb..s]  Sts[0280:.....]  Device  SCSI controller
```

此示例显示有关主总线上的设备的详细信息。 每行开头的两位数是设备号;后面的一位数字是函数号：

```dbgcmd
kd> !pci 1 0
PCI Bus 0
00:0  8086:1237.02  Cmd[0106:.mb..s]  Sts[2280:.....]  Device  Host bridge
      cf8:80000000  IntPin:0  IntLine:0  Rom:0  cis:0  cap:0

0d:0  8086:7000.01  Cmd[0007:imb...]  Sts[0280:.....]  Device  ISA bridge
      cf8:80006800  IntPin:0  IntLine:0  Rom:0  cis:0  cap:0

0d:1  8086:7010.00  Cmd[0005:i.b...]  Sts[0280:.....]  Device  IDE controller
      cf8:80006900  IntPin:0  IntLine:0  Rom:0  cis:0  cap:0
      IO[4]:fff1       

0e:0  1011:0021.02  Cmd[0107:imb..s]  Sts[0280:.....]  PciBridge 0->1-1  PCI-PCI bridge
      cf8:80007000  IntPin:0  IntLine:0  Rom:0  cap:0  2sts:2280  BCtrl:6 ISA
      IO:f000-ffff  Mem:fc000000-fdffffff  PMem:fff00000-fffff

10:0  102b:0519.01  Cmd[0083:im....]  Sts[0280:.....]  Device  VGA compatible controller
      cf8:80008000  IntPin:1  IntLine:9  Rom:80000000  cis:0  cap:0
      MEM[0]:fe800000  MPF[1]:fe000008  
```

此示例显示了有关总线 0 (零) 、设备0x0D 和函数0x1 的详细信息，包括来自0x00 和0x3F 之间的地址的原始 DWORD：

```dbgcmd
kd> !pci f 0 d 1 0 3f
PCI Bus 0
0d:1  8086:7010.00  Cmd[0005:i.b...]  Sts[0280:.....]  Device  IDE controller
      cf8:80006900  IntPin:0  IntLine:0  Rom:0  cis:0  cap:0
      IO[4]:fff1       
      00000000:  70108086 02800005 01018000 00002000
      00000010:  00000000 00000000 00000000 00000000
      00000020:  0000fff1 00000000 00000000 00000000
      00000030:  00000000 00000000 00000000 00000000
```

此示例显示段1、总线0、设备1的配置空间：

```dbgcmd
0: kd> !pci 301 1 0 1

PCI Configuration Space (Segment:0001 Bus:00 Device:01 Function:00)
Common Header:
    00: VendorID       14e4 Broadcom Corporation
    02: DeviceID       16c7
    04: Command        0146 MemSpaceEn BusInitiate PERREn SERREn
    06: Status         02b0 CapList 66MHzCapable FB2BCapable DEVSELTiming:1
.
.
.
    5a: MsgCtrl        64BitCapable MultipleMsgEnable:0 (0x1) MultipleMsgCapable:3 (0x8)
    5c: MsgAddr        2d4bff00
    60: MsgAddrHi      1ae09097
    64: MsData         9891
```

若要显示有效段上的所有设备和总线，请发出命令 **！ pci 602 ffff ff**：

```dbgcmd
0: kd> !pci 602 ffff ff
Scanning the following PCI segments: 0 0x1
PCI Segment 0 Bus 0
01:0  14e4:16c7.10  Cmd[0146:.mb.ps]  Sts[02b0:c6...]  Ethernet Controller  SubID:103c:1321
02:0  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
02:1  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
03:0  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
03:1  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
PCI Segment 0 Bus 0x38
01:0  14e4:1644.12  Cmd[0146:.mb.ps]  Sts[02b0:c6...]  Ethernet Controller  SubID:10b7:1000
PCI Segment 0 Bus 0x54
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0x54->0x55-0x55
PCI Segment 0 Bus 0x70
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0x70->0x71-0x71
PCI Segment 0 Bus 0xa9
01:0  8086:b154.00  Cmd[0147:imb.ps]  Sts[0ab0:c6.A.]  Intel PCI-PCI Bridge 0xa9->0xaa-0xaa
PCI Segment 0 Bus 0xaa
04:0  1033:0035.41  Cmd[0146:.mb.ps]  Sts[0210:c....]  NEC USB Controller  SubID:103c:1293
04:1  1033:0035.41  Cmd[0146:.mb.ps]  Sts[0210:c....]  NEC USB Controller  SubID:103c:aa55
04:2  1033:00e0.02  Cmd[0146:.mb.ps]  Sts[0210:c....]  NEC USB2 Controller  SubID:103c:aa55
05:0  1002:5159.00  Cmd[0187:imb..s]  Sts[0290:c....]  ATI VGA Compatible Controller  SubID:103c:1292
PCI Segment 0 Bus 0xc6
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0xc6->0xc7-0xc7
PCI Segment 0 Bus 0xe3
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0xe3->0xe4-0xe4
PCI Segment 0x1 Bus 0
01:0  14e4:16c7.10  Cmd[0146:.mb.ps]  Sts[02b0:c6...]  Ethernet Controller  SubID:103c:1321
02:0  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
02:1  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
03:0  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
03:1  1000:0030.08  Cmd[0147:imb.ps]  Sts[0230:c6...]  LSI SCSI Controller  SubID:103c:1323
PCI Segment 0x1 Bus 0x54
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0x54->0x55-0x55
PCI Segment 0x1 Bus 0x55
00:0  8086:10b9.06  Cmd[0147:imb.ps]  Sts[0010:c....]  Intel Ethernet Controller  SubID:8086:1083
PCI Segment 0x1 Bus 0x70
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0x70->0x71-0x71
PCI Segment 0x1 Bus 0xc6
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0xc6->0xc7-0xc7
PCI Segment 0x1 Bus 0xe3
00:0  103c:403b.00  Cmd[0547:imb.ps]  Sts[0010:c....]  HP PCI-PCI Bridge 0xe3->0xe4-0xe4
```









