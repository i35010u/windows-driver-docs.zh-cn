---
title: SerCx2 对象句柄
description: 本主题介绍专门为版本 2 的串行框架扩展 (SerCx2) 定义的对象句柄类型。
ms.localizationpriority: medium
ms.date: 12/27/2018
ms.openlocfilehash: b82a1e22366c31791cd86214ea098711e71edba1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520338"
---
# <a name="sercx2-object-handles"></a>SerCx2 对象句柄

本主题介绍专门为版本 2 的串行框架扩展 (SerCx2) 定义的对象句柄类型。 SerCx2 设备驱动程序接口 (DDI) 用法这些句柄来指代的功能和特定于 SerCx2 的功能的对象的类型。

此外，SerCx2 DDI 使用两个泛型对象句柄类型、 WDFDEVICE 和 WDFREQUEST，定义由内核模式驱动程序框架 (KMDF)。 有关框架句柄类型的详细信息，请参阅[Framework 对象摘要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)。

本主题介绍以下对象句柄：

* [SERCX2CUSTOMRECEIVE 对象句柄](#sercx2customreceive-object-handle)
* [SERCX2CUSTOMRECEIVETRANSACTION 对象句柄](#sercx2customreceivetransaction-object-handle)
* [SERCX2CUSTOMTRANSMIT 对象句柄](#sercx2customtransmit-object-handle)
* [SERCX2CUSTOMTRANSMITTRANSACTION 对象句柄](#sercx2customtransmittransaction-object-handle)
* [SERCX2PIORECEIVE 对象句柄](#sercx2pioreceive-object-handle)
* [SERCX2PIOTRANSMIT 对象句柄](#sercx2piotransmit-object-handle)
* [SERCX2SYSTEMDMARECEIVE 对象句柄](#sercx2systemdmareceive-object-handle)
* [SERCX2SYSTEMDMATRANSMIT 对象句柄](#sercx2systemdmatransmit-object-handle)

标头：2.0\Sercx.h

##  <a name="sercx2customreceive-object-handle"></a>SERCX2CUSTOMRECEIVE 对象句柄
一个**SERCX2CUSTOMRECEIVE**对象句柄是串行框架扩展 (SerCx2) 版本 2 中的 custom-receive 对象的不透明引用。

**SerCx2CustomReceiveCreate**方法创建 custom-receive 对象。 SerCx2 使用此对象来管理自定义的数据传输机制用于从串行控制器中读取数据的 I/O 事务。 此对象是不透明的串行控制器驱动程序。 
**SerCx2CustomReceiveCreate**提供，作为输出参数，为新创建的 SERCX2CUSTOMRECEIVE 句柄自定义接收对象。 SerCx2 和串行控制器驱动程序使用此句柄来指代 SerCx2 方法和事件的回调函数的后续调用中的对象。

之后**SerCx2CustomReceiveCreate**创建 custom-receive 对象，表示串行控制器设备的 framework 设备对象的生存期内存在此对象。 删除设备对象时，会自动删除 custom-receive 对象。 串行控制器驱动程序必须_不_尝试通过调用一个方法，如删除 custom-receive 对象[WdfObjectDelete](https://msdn.microsoft.com/library/windows/hardware/ff548734)。

串行控制器驱动程序可以作为一个选项，创建一个 custom-receive 对象，但可以创建多个此类对象。 该驱动程序可以创建此对象仅在以下情况下：

* 该驱动程序之前创建 PIO 接收对象。
* 该驱动程序有*不*创建了一个系统 DMA 接收的对象。

有关 PIO 接收对象的详细信息，请参阅[SERCX2PIORECEIVE 对象处理](#sercx2pioreceive-object-handle)。 有关系统 DMA 接收对象的详细信息，请参阅[SERCX2SYSTEMDMARECEIVE 对象处理](#sercx2systemdmareceive-object-handle)。


##  <a name="sercx2customreceivetransaction-object-handle"></a>SERCX2CUSTOMRECEIVETRANSACTION 对象句柄
一个**SERCX2CUSTOMRECEIVETRANSACTION**对象句柄是串行框架扩展 (SerCx2) 版本 2 中的自定义接收事务对象的不透明引用。

[SerCx2CustomReceiveTransactionCreate](https://msdn.microsoft.com/library/windows/hardware/dn265251)方法创建自定义接收事务对象。 SerCx2 使用此对象来管理自定义的数据传输机制用于读取由串行控制器接收的数据的 I/O 事务。 此对象是不透明的串行控制器驱动程序。 
[SerCx2CustomReceiveTransactionCreate](https://msdn.microsoft.com/library/windows/hardware/dn265251)作为输出参数，提供新创建的自定义接收事务对象的 SERCX2CUSTOMRECEIVETRANSACTION 句柄。 SerCx2 和这处理来指代中后续的对象的串行控制器驱动程序使用自定义接收事务。 有关详细信息，请参阅[SerCx2 自定义接收事务](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-custom-receive-transactions)。

之后[SerCx2CustomReceiveTransactionCreate](https://msdn.microsoft.com/library/windows/hardware/dn265251)创建自定义-接收-事务对象，表示串行控制器设备的 framework 设备对象的生存期内存在此对象。 删除设备对象时，会自动删除的自定义接收事务对象。 串行控制器驱动程序必须_不_尝试删除的自定义接收事务对象通过调用一个方法，如[WdfObjectDelete](https://msdn.microsoft.com/library/windows/hardware/ff548734)。

串行控制器驱动程序可以作为一个选项，创建自定义接收事务对象，但可以创建多个此类对象。 该驱动程序可以创建仅在以下情况下的此对象： < / wdcml:p >

* 该驱动程序之前创建 PIO 接收对象。
* 该驱动程序以前创建了一个 custom-receive 对象。

有关 PIO 接收对象的详细信息，请参阅[SERCX2PIORECEIVE 对象处理](#sercx2pioreceive-object-handle)。 有关详细信息自定义接收对象，请参阅[SERCX2CUSTOMRECEIVE 对象处理](#sercx2customreceive-object-handle)。

而类似 custom-receive 和自定义接收事务对象的生存期，无论这些定义为单独的对象类型 （并且不会合并为一种类型） 以支持 SerCx2 设备驱动程序接口可能将来扩展。

##  <a name="sercx2customtransmit-object-handle"></a>SERCX2CUSTOMTRANSMIT 对象句柄
SERCX2CUSTOMTRANSMIT 对象句柄是串行框架扩展 (SerCx2) 版本 2 中的 custom-transmit 对象的不透明引用。

[SerCx2CustomTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265256)方法创建自定义传输 object.h SerCx2 使用此对象管理将数据写入到串行控制器的 I/O 事务。 此对象是不透明的串行控制器驱动程序。 
[SerCx2CustomTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265256)提供，作为输出参数，为新创建的 SERCX2CUSTOMTRANSMIT 句柄自定义的传输对象。 SerCx2 和串行控制器驱动程序使用此句柄来指代 SerCx2 方法和事件的回调函数的后续调用中的对象。

之后[SerCx2CustomTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265256)创建 custom-transmit 对象，表示串行控制器设备的 framework 设备对象的生存期内存在此对象。 删除设备对象时，会自动删除 custom-transmit 对象。 串行控制器驱动程序必须_不_尝试通过调用一个方法，如删除 custom-transmit 对象[WdfObjectDelete](https://msdn.microsoft.com/library/windows/hardware/ff548734)。

串行控制器驱动程序可以作为一个选项，创建一个 custom-transmit 对象，但可以创建多个此类对象。 该驱动程序可以创建此对象仅在以下情况下：

* 该驱动程序之前创建 PIO 传输对象。
* 该驱动程序有_不_创建了一个系统 DMA 传输对象。

有关 PIO 传输对象的详细信息，请参阅[SERCX2PIOTRANSMIT 对象处理](#sercx2piotransmit-object-handle)。 有关系统 DMA 传输对象的详细信息，请参阅[SERCX2SYSTEMDMATRANSMIT 对象处理](#sercx2systemdmatransmit-object-handle)。

##  <a name="sercx2customtransmittransaction-object-handle"></a>SERCX2CUSTOMTRANSMITTRANSACTION 对象句柄
SERCX2CUSTOMTRANSMITTRANSACTION 对象句柄是串行框架扩展 (SerCx2) 版本 2 中的自定义传输的事务对象的不透明引用。

[SerCx2CustomTransmitTransactionCreate](https://msdn.microsoft.com/library/windows/hardware/dn265259)方法创建自定义传输的事务对象。 SerCx2 使用此对象来管理使用自定义的数据传输机制将数据写入串行控制器的 I/O 事务。 此对象是不透明的串行控制器驱动程序。 
[SerCx2CustomTransmitTransactionCreate](https://msdn.microsoft.com/library/windows/hardware/dn265259)作为输出参数，提供新创建的自定义传输的事务对象的 SERCX2CUSTOMTRANSMITTRANSACTION 句柄。 SerCx2 和这处理来指代中后续的对象的串行控制器驱动程序使用自定义的传输的事务。 有关详细信息，请参阅[SerCx2 自定义传输的事务](https://msdn.microsoft.com/library/windows/hardware/dn265320)。

之后[SerCx2CustomTransmitTransactionCreate](https://msdn.microsoft.com/library/windows/hardware/dn265259)创建自定义传输的事务对象，表示串行控制器设备的 framework 设备对象的生存期内存在此对象。 删除设备对象时，会自动删除的自定义传输的事务对象。 串行控制器驱动程序必须_不_尝试删除的自定义传输的事务对象通过调用一个方法，如[WdfObjectDelete](https://msdn.microsoft.com/library/windows/hardware/ff548734)。

串行控制器驱动程序可以作为一个选项，创建一个 custom-transmit 对象，但可以创建多个此类对象。 该驱动程序可以创建此对象仅在以下情况下：

* 该驱动程序之前创建 PIO 传输对象。
* 该驱动程序有_不_创建了一个系统 DMA 传输对象。

有关 PIO 传输对象的详细信息，请参阅[SERCX2PIOTRANSMIT 对象处理](#sercx2piotransmit-object-handle)。 有关详细信息自定义传输的对象，请参阅[SERCX2CUSTOMTRANSMIT 对象处理](#sercx2customtransmit-object-handle)。

而类似 custom-transmit 和自定义传输的事务对象的生存期，无论这些定义为单独的对象类型 （并且不会合并为一种类型） 以支持 SerCx2 设备驱动程序接口可能将来扩展。

##  <a name="sercx2pioreceive-object-handle"></a>SERCX2PIORECEIVE 对象句柄
SERCX2PIORECEIVE 对象句柄是串行框架扩展 (SerCx2) 版本 2 中的 PIO 接收对象的不透明引用。

[SerCx2PioReceiveCreate](https://msdn.microsoft.com/library/windows/hardware/dn265264)方法创建 PIO 接收对象。 SerCx2 使用对象来管理通过编程方式设置从串行控制器中读取数据的 I/O (PIO) 事务。 此对象是不透明的串行控制器驱动程序。 作为输出参数，提供新创建的 PIO 接收对象的 SERCX2PIORECEIVE 句柄。 SerCx2 和串行控制器驱动程序使用此句柄来引用后续 PIO 接收事务中的对象。 

有关详细信息，请参阅[SerCx2 PIO 接收事务](https://msdn.microsoft.com/library/windows/hardware/dn265332)。
之后[SerCx2PioReceiveCreate](https://msdn.microsoft.com/library/windows/hardware/dn265264)创建 PIO 接收对象，表示串行控制器设备的 framework 设备对象的生存期内存在此对象。 删除设备对象时，会自动删除 PIO 接收对象。 串行控制器驱动程序必须_不_尝试通过调用一个方法，如删除 PIO 接收对象[WdfObjectDelete](https://msdn.microsoft.com/library/windows/hardware/ff548734)。

串行控制器驱动程序必须创建一个且只有一个 PIO 接收的对象。 该驱动程序必须在创建系统 DMA 接收对象或 custom-receive 对象之前创建此对象。 有关系统 DMA 接收对象的详细信息，请参阅[SERCX2SYSTEMDMARECEIVE 对象处理](#sercx2systemdmareceive-object-handle)。 有关详细信息自定义接收对象，请参阅[SERCX2CUSTOMRECEIVE 对象处理](#sercx2customreceive-object-handle)。

##  <a name="sercx2piotransmit-object-handle"></a>SERCX2PIOTRANSMIT 对象句柄
SERCX2PIOTRANSMIT 对象句柄是串行框架扩展 (SerCx2) 版本 2 中 PIO 传输的对象的不透明引用。

[SerCx2PioTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265269)方法创建 PIO 传输对象。 SerCx2 使用此对象来管理使用编程 I/O (PIO) 将数据写入串行控制器的 I/O 事务。 此对象是不透明的串行控制器驱动程序。 
[SerCx2PioTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265269)作为输出参数，提供新创建的 PIO 传输对象的 SERCX2PIOTRANSMIT 句柄。 SerCx2 和串行控制器驱动程序使用此句柄来引用后续 PIO 传输的事务中的对象。 有关详细信息，请参阅[SerCx2 PIO 传输事务](https://msdn.microsoft.com/library/windows/hardware/dn265336)。


之后[SerCx2PioTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265269)创建 PIO 传输对象，表示串行控制器设备的 framework 设备对象的生存期内存在此对象。 删除设备对象时，会自动删除 PIO 传输对象。 串行控制器驱动程序必须_不_尝试通过调用一个方法，如删除 PIO 传输对象[WdfObjectDelete](https://msdn.microsoft.com/library/windows/hardware/ff548734)。

串行控制器驱动程序必须创建一个且只有一个 PIO 传输对象。 该驱动程序必须创建系统 DMA 传输对象或 custom-transmit 对象之前创建此对象。 有关系统 DMA 传输对象的详细信息，请参阅[SERCX2SYSTEMDMATRANSMIT 对象处理](#sercx2systemdmatransmit-object-handle)。 有关详细信息自定义传输的对象，请参阅[SERCX2CUSTOMTRANSMIT 对象处理](#sercx2customtransmit-object-handle)。

##  <a name="sercx2systemdmareceive-object-handle"></a>SERCX2SYSTEMDMARECEIVE 对象句柄
SERCX2SYSTEMDMARECEIVE 对象句柄是串行框架扩展 (SerCx2) 版本 2 中的系统 DMA 接收对象的不透明引用。

[SerCx2SystemDmaReceiveCreate](https://msdn.microsoft.com/library/windows/hardware/dn265279)方法创建系统 DMA 接收对象。 SerCx2 使用此对象来管理从串行控制器中读取数据的系统 DMA 事务。 此对象是不透明的串行控制器驱动程序。 
[SerCx2SystemDmaReceiveCreate](https://msdn.microsoft.com/library/windows/hardware/dn265279)作为输出参数，提供新创建的系统 DMA 接收对象的 SERCX2SYSTEMDMARECEIVE 句柄。 SerCx2 和串行控制器驱动程序使用此句柄来引用后续系统 DMA 接收事务中的对象。 有关详细信息，请参阅[SerCx2 系统 DMA 接收事务](https://msdn.microsoft.com/library/windows/hardware/dn265343)。

之后[SerCx2SystemDmaReceiveCreate](https://msdn.microsoft.com/library/windows/hardware/dn265279)创建系统-DMA-接收对象，表示串行控制器设备的 framework 设备对象的生存期内存在此对象。 删除设备对象时，会自动删除系统 DMA 接收对象。 串行控制器驱动程序可以作为一个选项，创建一个系统 DMA 接收对象，但可以创建多个此类对象。 该驱动程序可以创建此对象仅在以下情况下：

* 该驱动程序之前创建 PIO 接收对象。
* 该驱动程序有_不_创建了一个 custom-receive 对象。

有关 PIO 接收对象的详细信息，请参阅[SERCX2PIORECEIVE 对象处理](#sercx2pioreceive-object-handle)。 有关详细信息自定义接收对象，请参阅[SERCX2CUSTOMRECEIVE 对象处理](#sercx2customreceive-object-handle)。

##  <a name="sercx2systemdmatransmit-object-handle"></a>SERCX2SYSTEMDMATRANSMIT 对象句柄
SERCX2SYSTEMDMATRANSMIT 对象句柄是串行框架扩展 (SerCx2) 版本 2 中的系统 DMA 传输对象的不透明引用。

[SerCx2SystemDmaTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265288)方法创建系统 DMA 传输对象。 SerCx2 使用此对象来管理数据写入串行控制器的系统 DMA 事务。 此对象是不透明的串行控制器驱动程序。 
[SerCx2SystemDmaTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265288)作为输出参数，提供新创建的系统 DMA 传输对象的 SERCX2SYSTEMDMATRANSMIT 句柄。 SerCx2 和串行控制器驱动程序使用此句柄来引用后续系统 DMA 传输的事务中的对象。 有关详细信息，请参阅[SerCx2 系统 DMA 传输事务](https://msdn.microsoft.com/library/windows/hardware/dn265338)。

之后[SerCx2SystemDmaTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265288)创建系统-DMA 的传输对象，表示串行控制器设备的 framework 设备对象的生存期内存在此对象。 删除设备对象时，会自动删除系统 DMA 传输对象。 串行控制器驱动程序必须_不_尝试通过调用一个方法，如删除系统 DMA 传输对象[WdfObjectDelete](https://msdn.microsoft.com/library/windows/hardware/ff548734)。

串行控制器驱动程序可以作为一个选项，创建系统 DMA 传输的对象，但可以创建多个此类对象。 该驱动程序可以创建仅在以下情况下的此对象： < / wdcml:p >

* 该驱动程序之前创建 PIO 传输对象。
* 该驱动程序有_不_创建了一个 custom-transmit 对象。

有关 PIO 传输对象的详细信息，请参阅[SERCX2PIOTRANSMIT 对象处理](#sercx2piotransmit-object-handle)。 有关详细信息自定义传输的对象，请参阅[SERCX2CUSTOMTRANSMIT 对象处理](#sercx2customtransmit-object-handle)。

## <a name="related-topics"></a>相关主题

[SerCx2 自定义接收事务](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-custom-receive-transactions)

[SerCx2 自定义传输的事务](https://msdn.microsoft.com/library/windows/hardware/dn265320)

[SerCx2 PIO 接收事务](https://msdn.microsoft.com/library/windows/hardware/dn265332)

[SerCx2 PIO 传输的事务](https://msdn.microsoft.com/library/windows/hardware/dn265336)

[SerCx2 系统 DMA 接收事务](https://msdn.microsoft.com/library/windows/hardware/dn265343)

[SerCx2 系统 DMA 传输的事务](https://msdn.microsoft.com/library/windows/hardware/dn265338)

[SerCx2CustomReceiveTransactionCreate](https://msdn.microsoft.com/library/windows/hardware/dn265251)

[SerCx2CustomTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265256)

[SerCx2CustomTransmitTransactionCreate](https://msdn.microsoft.com/library/windows/hardware/dn265259)

[SerCx2PioReceiveCreate](https://msdn.microsoft.com/library/windows/hardware/dn265264)

[SerCx2PioReceiveCreate](https://msdn.microsoft.com/library/windows/hardware/dn265264)

[SerCx2PioTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265269)

[SerCx2SystemDmaReceiveCreate](https://msdn.microsoft.com/library/windows/hardware/dn265279)

[SerCx2SystemDmaTransmitCreate](https://msdn.microsoft.com/library/windows/hardware/dn265288)

[Framework 对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)

[WdfObjectDelete](https://msdn.microsoft.com/library/windows/hardware/ff548734)





