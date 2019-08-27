---
title: dma
description: Dma 扩展显示有关直接内存访问 (DMA) 子系统和驱动程序验证程序的 DMA 验证程序选项的信息。
ms.assetid: 4ccf679f-5804-4644-935a-18ff8711ae9a
keywords:
- DMA 验证 (驱动程序验证程序)
- dma Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dma
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1d4a83031e8d8b568f93c92d8b8cdd95b741187
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025275"
---
# <a name="dma"></a>!dma


**! Dma**扩展显示有关直接内存访问 (dma) 子系统和驱动程序验证程序的**dma 验证**程序选项的信息。

```dbgcmd
!dma 
!dma Adapter [Flags]
```

## <a name="span-idddk__dma_pgspanspan-idddk__dma_pgspanparameters"></a><span id="ddk__dma_pg"></span><span id="DDK__DMA_PG"></span>Parameters


<span id="_______Adapter______"></span><span id="_______adapter______"></span><span id="_______ADAPTER______"></span>*适配器*   
指定要显示的 DMA 适配器的十六进制地址。 如果此值为零, 则将显示所有 DMA 适配器。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要包含在显示中的信息。 这可以是以下位的任意组合。 默认值为0x1。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
使显示内容包括一般适配器信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
使显示内容包括映射寄存器信息。 (仅当 DMA 验证处于活动状态时)。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
使显示内容包括常见的缓冲区信息。 (仅当 DMA 验证处于活动状态时)。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
使显示内容包括散播/聚集列表信息。 (仅当 DMA 验证处于活动状态时)。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)  
使显示包含硬件设备的设备说明。 (仅当 DMA 验证处于活动状态时)。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>位 5 (0x20)  
使显示包括等待上下文块信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关驱动程序验证程序的信息, 请参阅 Windows 驱动程序工具包 (WDK) 文档。 有关 DMA 的信息, 请参阅 Windows 驱动程序工具包 (WDK) 文档和*Microsoft Windows 内部*内容, 标记 Russinovich David 所罗门群岛。

<a name="remarks"></a>备注
-------

参数无效 (例如, **! dma 1**) 生成简短的帮助文本。

如果 **! dma**扩展与 no 参数一起使用, 则它将显示所有 dma 适配器及其地址的简洁列表。 这可用于获取适配器的地址, 以便在此命令的较长版本中使用。

下面的示例演示了驱动程序验证程序的**DMA 验证**选项处于活动状态时, 如何使用此扩展:

```dbgcmd
0:kd> !dma

Dumping all DMA adapters...

Adapter: 82faebd0     Owner: SCSIPORT!ScsiPortGetUncachedExtension 
Adapter: 82f88930     Owner: SCSIPORT!ScsiPortGetUncachedExtension 
Adapter: 82f06cd0     Owner: NDIS!NdisMAllocateMapRegisters 
Master adapter: 80076800
```

在此输出中, 可以看到系统中有三个 DMA 适配器。 SCSIPORT 拥有两个, NDIS 拥有第三个。 若要详细检查 NDIS 适配器, 请使用 **! dma**扩展, 其地址为:

```dbgcmd
0:kd> !dma  82f06cd0
Adapter: 82f06cd0     Owner: NDIS!NdisMAllocateMapRegisters (0x9fe24351)
 MasterAdapter:       00000000
   Adapter base Va      00000000
   Map register base:   00000000
 WCB:                 82f2b604
   Map registers: 00000000 mapped, 00000000 allocated, 00000002 max

   Dma verifier additional information:
   DeviceObject: 82f98690
   Map registers:        00000840 allocated, 00000000 freed
   Scatter-gather lists: 00000000 allocated, 00000000 freed
   Common buffers:       00000004 allocated, 00000000 freed
   Adapter channels:     00000420 allocated, 00000420 freed
   Bytes mapped since last flush: 000000f2
```

第一个数据块是 HAL 开发人员可用于调试问题的特定信息。 出于您的目的, "Dma 验证程序附加信息" 下面的数据是很有趣的。 在此示例中, 将看到 NDIS 已分配0x840 映射寄存器。 这是一个非常大的数字, 尤其是因为 NDIS 指出它计划最多使用两个映射寄存器。 此适配器明显不使用散点/收集列表, 并已将其置于所有适配器通道。 更详细地查看地图注册:

```dbgcmd
0:kd> !dma  82f06cd0 2
Adapter: 82f06cd0     Owner: NDIS!NdisMAllocateMapRegisters 
...

  Map register file 82f06c58 (0/2 mapped)
     Double buffer mdl: 82f2c188
     Map registers:
        82f06c80: Not mapped
        82f06c8c: Not mapped

  Map register file 82f06228 (1/2 mapped)
     Double buffer mdl: 82f1b678
     Map registers:
        82f06250: 00bc bytes mapped to f83c003c
        82f0625c: Not mapped

  Map register file 82fa5ad8 (1/2 mapped)
     Double buffer mdl: 82f1b048
     Map registers:
        82fa5b00: 0036 bytes mapped to 82d17102
        82fa5b0c: Not mapped
...
```

在此示例中, 你将看到某些映射寄存器已映射。 每个*映射注册文件*都是由驱动程序分配的映射寄存器。 换言之, 它代表对**AllocateAdapterChannel**的单一调用。 NDIS 收集大量这些映射寄存器文件, 而某些驱动程序一次创建一个, 并在它们完成时释放它们。

Map register 文件也是返回到名称为 "MapRegisterBase" 的设备的地址。 请注意, DMA 验证器仅挂接每个驱动程序的前64映射寄存器。 由于空间的原因 (每个地图寄存器表示三个物理页面), 其余部分将被忽略。

在此示例中, 两个地图注册文件正在使用中。 这意味着该驱动程序已映射缓冲区, 因此它对硬件可见。 在第一种情况下, 0xBC 字节映射到系统虚拟地址0xF83C003C。

常见缓冲区的检查将显示:

```dbgcmd
0:kd> !dma  82f06cd0 4
Adapter: 82f06cd0     Owner: NDIS!NdisMAllocateMapRegisters 
...
   Common buffer allocated by NDIS!NdisMAllocateSharedMemory:
      Length:           1000
      Virtual address:  82e77000
      Physical address: 2a77000

   Common buffer allocated by NDIS!NdisMAllocateSharedMemory:
      Length:           12010
      Virtual address:  82e817f8
      Physical address: 2a817f8

   Common buffer allocated by NDIS!NdisMAllocateSharedMemory:
      Length:           4300
      Virtual address:  82e95680
      Physical address: 2a95680

   Common buffer allocated by NDIS!NdisMAllocateSharedMemory:
      Length:           4800
      Virtual address:  82e9d400
      Physical address: 2a9d400
```

这相当简单;存在四个不同长度的常见缓冲区。 同时提供物理和虚拟地址。

 

 





