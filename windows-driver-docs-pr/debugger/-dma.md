---
title: dma
description: Dma 扩展显示有关直接内存访问 (DMA) 子系统和驱动程序验证程序的 DMA Verifier 选项的信息。
ms.assetid: 4ccf679f-5804-4644-935a-18ff8711ae9a
keywords:
- DMA 验证 （驱动程序验证程序）
- dma Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dma
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 87d2e51a4c4170d2d4a22b91b52d3802270b4546
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334568"
---
# <a name="dma"></a>!dma


**！ Dma**扩展显示信息的直接内存访问 (DMA) 子系统，并**DMA Verifier** Driver Verifier 选项。

```dbgcmd
!dma 
!dma Adapter [Flags]
```

## <a name="span-idddkdmapgspanspan-idddkdmapgspanparameters"></a><span id="ddk__dma_pg"></span><span id="DDK__DMA_PG"></span>参数


<span id="_______Adapter______"></span><span id="_______adapter______"></span><span id="_______ADAPTER______"></span> *Adapter*   
指定要显示的 DMA 适配器的十六进制地址。 如果这是零，将显示所有 DMA 适配器。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要包括在显示的信息。 这可以是以下位的任意组合。 默认值为 0x1。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
将导致显示以包括泛型适配器的信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
将导致显示以包括映射注册信息。 （仅当 DMA 验证处于活动状态。）

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
将导致显示以包括常见的缓冲区信息。 （仅当 DMA 验证处于活动状态。）

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
将导致显示以包括散播-聚集列表信息。 （仅当 DMA 验证处于活动状态。）

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
将导致显示以包括硬件设备的设备说明。 （仅当 DMA 验证处于活动状态。）

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>5 位 (0x20)  
将导致显示以包括等待上下文块信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关驱动程序验证程序的信息，请参阅 Windows Driver Kit (WDK) 文档。 DMA 有关的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich David Solomon。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

参数无效 (例如， **！ dma 1**) 生成简要的帮助文本。

当 **！ dma**扩展使用不带任何参数，则会显示所有 DMA 适配器及其地址的简明列表。 这可以用于获取在此命令的更长的版本中使用的适配器的地址。

下面是此扩展可以是如何的示例时使用 Driver Verifier **DMA 验证**选项处于活动状态：

```dbgcmd
0:kd> !dma

Dumping all DMA adapters...

Adapter: 82faebd0     Owner: SCSIPORT!ScsiPortGetUncachedExtension 
Adapter: 82f88930     Owner: SCSIPORT!ScsiPortGetUncachedExtension 
Adapter: 82f06cd0     Owner: NDIS!NdisMAllocateMapRegisters 
Master adapter: 80076800
```

在此输出中，可以看到系统中有三个 DMA 适配器。 SCSIPORT 拥有两个，NDIS 拥有第三个。 若要检查的 NDIS 适配器中详细信息，请使用 **！ dma**用其地址的扩展：

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

第一个数据块是 HAL 开发人员可用于调试问题的特定信息。 对您而言，"Dma verifier 其他信息"下面的数据是我们的兴趣。 在此示例中，可以看到 NDIS 已经分配了 0x840 映射寄存器。 这是很多，尤其是因为 NDIS 有指示其计划使用的最大的两个映射寄存器。 此适配器显然不使用散播-聚集列表，并已将消失及其所有适配器频道。 查看更多详细信息中的地图寄存器内容：

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

在此示例中，可以看到某些映射寄存器已映射。 每个*映射注册文件*的驱动程序映射寄存器分配。 换而言之，它表示调用一次**AllocateAdapterChannel**。 NDIS 收集大量的这些映射的注册文件，而某些驱动程序创建一个在时间和处置它们将完成。

映射注册文件也是返回给设备名称"MapRegisterBase"下的地址。 请注意 DMA 验证工具仅挂钩每个驱动程序的前 64 映射寄存器。 其余部分会忽略的空间 （每个映射注册表示三个物理页） 的原因。

在此示例中，两个映射文件正在使用的寄存器。 这意味着该驱动程序已映射的缓冲区，使其可见的硬件。 在第一种情况下，0xBC 字节映射到系统虚拟地址 0xF83C003C。

常见的缓冲区检查就会发现：

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

这是非常简单;有四个常见缓冲区长度不同。 所有指定的物理和虚拟地址。

 

 





