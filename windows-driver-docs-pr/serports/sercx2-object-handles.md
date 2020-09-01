---
title: SerCx2 对象句柄
description: 本主题介绍专门为版本2的串行框架扩展 (SerCx2) 定义的对象句柄类型。
ms.localizationpriority: medium
ms.date: 12/27/2018
ms.openlocfilehash: 86be17afbc95c817110bd53cb6e970a5e4d24639
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186917"
---
# <a name="sercx2-object-handles"></a>SerCx2 对象句柄

本主题介绍专门为版本2的串行框架扩展 (SerCx2) 定义的对象句柄类型。 SerCx2 设备驱动程序接口 (DDI) 使用这些句柄类型引用具有特定于 SerCx2 的特性和功能的对象。

此外，SerCx2 DDI 使用内核模式驱动程序框架所定义的两个泛型对象句柄类型 WDFDEVICE 和 WDFREQUEST (KMDF) 。 有关框架句柄类型的详细信息，请参阅 [框架对象的摘要](../wdf/summary-of-framework-objects.md)。

本主题介绍下列对象句柄：

* [SERCX2CUSTOMRECEIVE 对象句柄](#sercx2customreceive-object-handle)
* [SERCX2CUSTOMRECEIVETRANSACTION 对象句柄](#sercx2customreceivetransaction-object-handle)
* [SERCX2CUSTOMTRANSMIT 对象句柄](#sercx2customtransmit-object-handle)
* [SERCX2CUSTOMTRANSMITTRANSACTION 对象句柄](#sercx2customtransmittransaction-object-handle)
* [SERCX2PIORECEIVE 对象句柄](#sercx2pioreceive-object-handle)
* [SERCX2PIOTRANSMIT 对象句柄](#sercx2piotransmit-object-handle)
* [SERCX2SYSTEMDMARECEIVE 对象句柄](#sercx2systemdmareceive-object-handle)
* [SERCX2SYSTEMDMATRANSMIT 对象句柄](#sercx2systemdmatransmit-object-handle)

标头： 2.0 \ Sercx

##  <a name="sercx2customreceive-object-handle"></a>SERCX2CUSTOMRECEIVE 对象句柄
**SERCX2CUSTOMRECEIVE**对象句柄是对) 的串行 framework (扩展的版本2中的自定义接收对象的不透明引用。

**SerCx2CustomReceiveCreate**方法创建自定义接收对象。 SerCx2 使用此对象管理使用自定义数据传输机制从串行控制器读取数据的 i/o 事务。 此对象对串行控制器驱动程序是不透明的。 
作为输出参数， **SerCx2CustomReceiveCreate**提供给新创建的自定义接收对象的 SERCX2CUSTOMRECEIVE 句柄。 SerCx2 和串行控制器驱动程序使用此句柄在对 SerCx2 方法和事件回调函数的后续调用中引用对象。

**SerCx2CustomReceiveCreate**创建自定义接收对象后，此对象存在于表示串行控制器设备的框架设备对象的生存期内。 删除设备对象时，会自动删除自定义接收对象。 串行控制器驱动程序不得 _尝试通过_ 调用方法（如 [WdfObjectDelete](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)）删除自定义接收对象。

串行控制器驱动程序可作为选项创建自定义接收对象，但不能创建多个这样的对象。 此驱动程序只能在以下条件下创建此对象：

* 驱动程序以前创建了一个 PIO 接收对象。
* 驱动程序 *未* 创建系统 DMA 接收对象。

有关 PIO 接收对象的详细信息，请参阅 [SERCX2PIORECEIVE 对象句柄](#sercx2pioreceive-object-handle)。 有关系统 DMA 接收对象的详细信息，请参阅 [SERCX2SYSTEMDMARECEIVE 对象句柄](#sercx2systemdmareceive-object-handle)。


##  <a name="sercx2customreceivetransaction-object-handle"></a>SERCX2CUSTOMRECEIVETRANSACTION 对象句柄
**SERCX2CUSTOMRECEIVETRANSACTION**对象句柄是对) 的串行 framework (扩展的版本2中的自定义接收事务对象的不透明引用。

[SerCx2CustomReceiveTransactionCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncreate)方法创建自定义接收事务对象。 SerCx2 使用此对象管理使用自定义数据传输机制读取串行控制器接收的数据的 i/o 事务。 此对象对串行控制器驱动程序是不透明的。 
[SerCx2CustomReceiveTransactionCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncreate) 作为输出参数提供给新创建的自定义接收事务对象的 SERCX2CUSTOMRECEIVETRANSACTION 句柄。 SerCx2 和串行控制器驱动程序使用此句柄来引用后续自定义接收事务中的对象。 有关详细信息，请参阅 [SerCx2 自定义接收事务](./sercx2-custom-receive-transactions.md)。

[SerCx2CustomReceiveTransactionCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncreate)创建自定义接收事务对象后，此对象存在于表示串行控制器设备的框架设备对象的生存期内。 删除设备对象时，会自动删除自定义接收-事务对象。 串行控制器驱动程序不得 _尝试通过_ 调用方法（如 [WdfObjectDelete](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)）删除自定义接收事务对象。

串行控制器驱动程序可作为选项创建自定义接收-事务对象，但不能创建多个这样的对象。 此驱动程序只能在以下条件下创建此对象： </wdcml： p>

* 驱动程序以前创建了一个 PIO 接收对象。
* 驱动程序以前创建了一个自定义接收对象。

有关 PIO 接收对象的详细信息，请参阅 [SERCX2PIORECEIVE 对象句柄](#sercx2pioreceive-object-handle)。 有关自定义接收对象的详细信息，请参阅 [SERCX2CUSTOMRECEIVE 对象句柄](#sercx2customreceive-object-handle)。

尽管自定义接收和自定义接收事务对象具有相似的生存期，但它们被定义为单独的对象类型 (并且不组合到一种类型) 中，以支持将来 SerCx2 设备驱动程序接口的扩展。

##  <a name="sercx2customtransmit-object-handle"></a>SERCX2CUSTOMTRANSMIT 对象句柄
SERCX2CUSTOMTRANSMIT 对象句柄是对) 的串行 framework (扩展的版本2中的自定义传输对象的不透明引用。

[SerCx2CustomTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmitcreate)方法创建自定义传输对象。 h SerCx2 使用此对象管理将数据写入串行控制器的 i/o 事务。 此对象对串行控制器驱动程序是不透明的。 
作为输出参数， [SerCx2CustomTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmitcreate)提供给新创建的自定义传输对象的 SERCX2CUSTOMTRANSMIT 句柄。 SerCx2 和串行控制器驱动程序使用此句柄在对 SerCx2 方法和事件回调函数的后续调用中引用对象。

在 [SerCx2CustomTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmitcreate) 创建自定义传输对象后，此对象存在于表示串行控制器设备的框架设备对象的生存期内。 删除设备对象时，会自动删除自定义传输对象。 串行控制器驱动程序不得 _尝试通过_ 调用方法（如 [WdfObjectDelete](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)）删除自定义传输对象。

串行控制器驱动程序可作为选项创建自定义传输对象，但不能创建多个这样的对象。 此驱动程序只能在以下条件下创建此对象：

* 驱动程序先前创建了 PIO 传输对象。
* 驱动程序 _未_ 创建系统 DMA 传输对象。

有关 PIO 传输对象的详细信息，请参阅 [SERCX2PIOTRANSMIT 对象句柄](#sercx2piotransmit-object-handle)。 有关系统 DMA 传输对象的详细信息，请参阅 [SERCX2SYSTEMDMATRANSMIT 对象句柄](#sercx2systemdmatransmit-object-handle)。

##  <a name="sercx2customtransmittransaction-object-handle"></a>SERCX2CUSTOMTRANSMITTRANSACTION 对象句柄
SERCX2CUSTOMTRANSMITTRANSACTION 对象句柄是对) 的串行 framework (扩展的版本2中的自定义传输事务对象的不透明引用。

[SerCx2CustomTransmitTransactionCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncreate)方法创建自定义传输事务对象。 SerCx2 使用此对象管理使用自定义数据传输机制将数据写入串行控制器的 i/o 事务。 此对象对串行控制器驱动程序是不透明的。 
作为输出参数， [SerCx2CustomTransmitTransactionCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncreate)提供给新创建的自定义传输事务对象的 SERCX2CUSTOMTRANSMITTRANSACTION 句柄。 SerCx2 和串行控制器驱动程序使用此句柄来引用后续自定义传输事务中的对象。 有关详细信息，请参阅 [SerCx2 自定义传输事务](/previous-versions/dn265320(v=vs.85))。

在 [SerCx2CustomTransmitTransactionCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncreate) 创建自定义传输事务对象后，此对象存在于表示串行控制器设备的框架设备对象的生存期内。 删除设备对象时，会自动删除自定义传输事务对象。 串行控制器驱动程序不得 _尝试通过_ 调用方法（如 [WdfObjectDelete](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)）删除自定义传输事务对象。

串行控制器驱动程序可作为选项创建自定义传输对象，但不能创建多个这样的对象。 此驱动程序只能在以下条件下创建此对象：

* 驱动程序先前创建了 PIO 传输对象。
* 驱动程序 _未_ 创建系统 DMA 传输对象。

有关 PIO 传输对象的详细信息，请参阅 [SERCX2PIOTRANSMIT 对象句柄](#sercx2piotransmit-object-handle)。 有关自定义传输对象的详细信息，请参阅 [SERCX2CUSTOMTRANSMIT 对象句柄](#sercx2customtransmit-object-handle)。

尽管自定义传输和自定义传输事务对象具有相似的生存期，但它们被定义为单独的对象类型 (并且不组合到一种类型) 中，以支持将来 SerCx2 设备驱动程序接口的扩展。

##  <a name="sercx2pioreceive-object-handle"></a>SERCX2PIORECEIVE 对象句柄
SERCX2PIORECEIVE 对象句柄是对) 的串行 framework (扩展的版本2中的 PIO 接收对象的不透明引用。

[SerCx2PioReceiveCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecreate)方法创建一个 PIO 接收对象。 SerCx2 使用对象管理从串行控制器读取数据的程控 (PIO) 事务。 此对象对串行控制器驱动程序是不透明的。 作为输出参数提供给新创建的 PIO 接收对象的 SERCX2PIORECEIVE 句柄。 SerCx2 和串行控制器驱动程序使用此句柄来引用后面的 PIO 接收事务中的对象。 

有关详细信息，请参阅 [SERCX2 PIO-接收事务](/previous-versions/dn265332(v=vs.85))。
[SerCx2PioReceiveCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecreate)创建了 PIO 接收对象后，此对象存在于表示串行控制器设备的框架设备对象的生存期内。 删除设备对象时，会自动删除 PIO 接收对象。 串行控制器驱动程序不得 _尝试通过_ 调用方法（如 [WDFOBJECTDELETE](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)）删除 PIO 接收对象。

串行控制器驱动程序必须仅创建一个 PIO 接收对象。 在创建系统 DMA 接收对象或自定义接收对象之前，驱动程序必须创建此对象。 有关系统 DMA 接收对象的详细信息，请参阅 [SERCX2SYSTEMDMARECEIVE 对象句柄](#sercx2systemdmareceive-object-handle)。 有关自定义接收对象的详细信息，请参阅 [SERCX2CUSTOMRECEIVE 对象句柄](#sercx2customreceive-object-handle)。

##  <a name="sercx2piotransmit-object-handle"></a>SERCX2PIOTRANSMIT 对象句柄
SERCX2PIOTRANSMIT 对象句柄是对) 的串行 framework (扩展的版本2中的 PIO 传输对象的不透明引用。

[SerCx2PioTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcreate)方法创建 PIO 传输对象。 SerCx2 使用此对象管理使用程控 i/o (PIO) 将数据写入串行控制器的 i/o 事务。 此对象对串行控制器驱动程序是不透明的。 
[SerCx2PioTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcreate) 作为输出参数提供给新创建的 PIO 传输对象的 SERCX2PIOTRANSMIT 句柄。 SerCx2 和串行控制器驱动程序使用此句柄来引用后续 PIO 传输事务中的对象。 有关详细信息，请参阅 [SERCX2 PIO-传输事务](/previous-versions/dn265336(v=vs.85))。


在 [SerCx2PioTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcreate) 创建了 PIO 传输对象后，此对象存在于表示串行控制器设备的框架设备对象的生存期内。 删除设备对象时，会自动删除 PIO 传输对象。 串行控制器驱动程序不得 _尝试通过_ 调用方法（如 [WDFOBJECTDELETE](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)）删除 PIO 传输对象。

串行控制器驱动程序必须仅创建一个 PIO 传输对象。 在创建系统 DMA 传输对象或自定义传输对象之前，驱动程序必须创建此对象。 有关系统 DMA 传输对象的详细信息，请参阅 [SERCX2SYSTEMDMATRANSMIT 对象句柄](#sercx2systemdmatransmit-object-handle)。 有关自定义传输对象的详细信息，请参阅 [SERCX2CUSTOMTRANSMIT 对象句柄](#sercx2customtransmit-object-handle)。

##  <a name="sercx2systemdmareceive-object-handle"></a>SERCX2SYSTEMDMARECEIVE 对象句柄
SERCX2SYSTEMDMARECEIVE 对象句柄是对版本2中的系统 DMA 接收对象的不透明引用， (SerCx2) 。

[SerCx2SystemDmaReceiveCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecreate)方法创建系统 DMA 接收对象。 SerCx2 使用此对象管理从串行控制器读取数据的系统 DMA 事务。 此对象对串行控制器驱动程序是不透明的。 
作为输出参数， [SerCx2SystemDmaReceiveCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecreate)提供给新创建的系统 DMA 接收对象的 SERCX2SYSTEMDMARECEIVE 句柄。 SerCx2 和串行控制器驱动程序使用此句柄来引用后续的系统 DMA 接收事务中的对象。 有关详细信息，请参阅 [SerCx2](/previous-versions/dn265343(v=vs.85))。

[SerCx2SystemDmaReceiveCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecreate)创建系统 DMA 接收对象后，此对象存在于表示串行控制器设备的框架设备对象的生存期内。 删除设备对象时，系统将自动删除系统 DMA 接收对象。 串行控制器驱动程序可以选择创建系统 DMA 接收对象，但不能创建多个这样的对象。 此驱动程序只能在以下条件下创建此对象：

* 驱动程序以前创建了一个 PIO 接收对象。
* 驱动程序 _未_ 创建自定义接收对象。

有关 PIO 接收对象的详细信息，请参阅 [SERCX2PIORECEIVE 对象句柄](#sercx2pioreceive-object-handle)。 有关自定义接收对象的详细信息，请参阅 [SERCX2CUSTOMRECEIVE 对象句柄](#sercx2customreceive-object-handle)。

##  <a name="sercx2systemdmatransmit-object-handle"></a>SERCX2SYSTEMDMATRANSMIT 对象句柄
SERCX2SYSTEMDMATRANSMIT 对象句柄是对版本2中的系统 DMA 传输对象的不透明引用， (SerCx2) 。

[SerCx2SystemDmaTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcreate)方法创建系统 DMA 传输对象。 SerCx2 使用此对象管理系统 DMA 事务，这些事务将数据写入串行控制器。 此对象对串行控制器驱动程序是不透明的。 
作为输出参数， [SerCx2SystemDmaTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcreate)提供给新创建的系统 DMA 传输对象的 SERCX2SYSTEMDMATRANSMIT 句柄。 SerCx2 和串行控制器驱动程序使用此句柄来引用后续的系统 DMA 传输事务中的对象。 有关详细信息，请参阅 [SerCx2](/previous-versions/dn265338(v=vs.85))。

[SerCx2SystemDmaTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcreate)创建系统 DMA 传输对象后，此对象在表示串行控制器设备的框架设备对象的生存期内存在。 删除设备对象时，系统将自动删除 "系统 DMA 传输" 对象。 串行控制器驱动程序不得 _尝试通过_ 调用 [WdfObjectDelete](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)等方法删除系统 DMA 传输对象。

串行控制器驱动程序可以选择创建系统 DMA 传输对象，但不能创建多个这样的对象。 此驱动程序只能在以下条件下创建此对象： </wdcml： p>

* 驱动程序先前创建了 PIO 传输对象。
* 驱动程序 _未_ 创建自定义传输对象。

有关 PIO 传输对象的详细信息，请参阅 [SERCX2PIOTRANSMIT 对象句柄](#sercx2piotransmit-object-handle)。 有关自定义传输对象的详细信息，请参阅 [SERCX2CUSTOMTRANSMIT 对象句柄](#sercx2customtransmit-object-handle)。

## <a name="related-topics"></a>相关主题

[SerCx2 Custom-Receive 事务](./sercx2-custom-receive-transactions.md)

[SerCx2 Custom-Transmit 事务](/previous-versions/dn265320(v=vs.85))

[SerCx2 PIO-Receive 事务](/previous-versions/dn265332(v=vs.85))

[SerCx2 PIO-Transmit 事务](/previous-versions/dn265336(v=vs.85))

[SerCx2 System-DMA-Receive 事务](/previous-versions/dn265343(v=vs.85))

[SerCx2 System-DMA-Transmit 事务](/previous-versions/dn265338(v=vs.85))

[SerCx2CustomReceiveTransactionCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncreate)

[SerCx2CustomTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmitcreate)

[SerCx2CustomTransmitTransactionCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncreate)

[SerCx2PioReceiveCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecreate)

[SerCx2PioReceiveCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecreate)

[SerCx2PioTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcreate)

[SerCx2SystemDmaReceiveCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecreate)

[SerCx2SystemDmaTransmitCreate](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcreate)

[框架对象摘要](../wdf/summary-of-framework-objects.md)

[WdfObjectDelete](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)