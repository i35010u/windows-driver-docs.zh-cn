---
title: 微型驱动程序控制流
description: 微型驱动程序控制流
ms.assetid: c3c23d32-4023-445b-bd89-e0b454bec1ed
keywords:
- Flow 类驱动程序 WDK Windows 2000 内核，控制流
- 流式传输微型驱动程序 WDK Windows 2000 内核，控制流
- 微型驱动程序 WDK Windows 2000 内核流式处理，控制流
- 未初始化流式处理微型驱动程序 WDK 流式处理微型驱动程序
- 初始化流式处理微型驱动程序 WDK Windows 2000 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38e6a1eb3b114cebe51eb41d59f8a8781064ec95
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842137"
---
# <a name="minidriver-flow-of-control"></a>微型驱动程序控制流





以下一组步骤通常遵循初始化、使用和取消初始化流式处理微型驱动程序。 本文档的其他部分介绍了以下引用的命令和结构。

**在初始化、使用和取消初始化流式处理微型驱动程序时遵循的步骤如下**

1.  即插即用枚举器检测到微型驱动程序支持的硬件适配器。 枚举器检查注册表以解析任何符号引用，并将请求传递给 i/o 子系统。

2.  I/o 子系统将加载微型驱动程序并调用微型驱动程序的**DriverEntry**例程（请参阅[**DriverEntry For Stream Class 微型驱动程序**](https://docs.microsoft.com/previous-versions/ff558717(v=vs.85))），其中\_数据结构分配和初始化[**HW\_初始化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)。 文件对象是从**DriverEntry**例程中的信息创建的。

3.  然后，微型驱动程序的**DriverEntry**例程调用 stream 类驱动程序的[**StreamClassRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)函数并将[**HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)结构作为参数传递。 \_数据结构的 HW\_初始化包含处理 SRBs 的微型驱动程序函数的地址。 这允许微型驱动程序响应类驱动程序发送的 SRBs。

4.  在初始化期间，stream 类驱动程序将在[**HW\_初始化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)中指定的函数\_数据结构的**HwReceivePacket**成员（请参阅[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)）以及 SRB**和命令**成员设置为 SRB\_初始化\_设备。 然后，微型驱动程序初始化硬件适配器。

5.  流类驱动程序调用\_HW 中指定的函数[ **\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)结构的**HWRECEIVEPACKET**成员与 SRB\_获取\_流\_信息。 然后，微型驱动程序返回有关它所支持的流的信息。

6.  流类驱动程序调用 **\_hw**中指定的函数\_数据结构的**HWRECEIVEPACKET**成员与 SRB\_OPEN\_Stream，并使用[**hw\_stream\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object)构造. 微型驱动程序执行必要的硬件操作以打开指定的流。

7.  Stream 类驱动程序通过传递 SRB\_读取\_数据或 SRB\_将\_数据命令写入到 HW\_流的**ReceiveDataPacket**成员中指定的函数，发送或请求流中的数据\_流的对象结构。

8.  Stream 类驱动程序通过将相应的流请求块（[**HW\_stream\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)）传递给在中**指定的函数来获取和设置流的属性和其他控制信息。ReceiveControlPacket**\_流的对象结构的 HW\_流的成员。

9.  当系统通过使用流时，stream 类驱动程序会调用\_HW 中指定的函数[ **\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)结构的**HWRECEIVEPACKET**成员与 SRB\_CLOSE\_流。 然后，微型驱动程序将关闭指定的流。

10. 当需要取消对适配器的初始化时，stream 类驱动程序会调用\_HW 中指定的函数[ **\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)结构的**HWRECEIVEPACKET**成员与 SRB\_取消初始化\_设备。 然后，微型驱动程序取消设备。

 

 




