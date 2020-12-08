---
title: 微型驱动程序控制流
description: 微型驱动程序控制流
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，控制流
- 流式传输微型驱动程序 WDK Windows 2000 内核，控制流
- 微型驱动程序 WDK Windows 2000 内核流式处理，控制流
- 未初始化流式处理微型驱动程序 WDK 流式处理微型驱动程序
- 初始化流式处理微型驱动程序 WDK Windows 2000 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 644c98dc30e354569ff30740ea8bc42d027d2264
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833279"
---
# <a name="minidriver-flow-of-control"></a>微型驱动程序控制流





以下一组步骤通常遵循初始化、使用和取消初始化流式处理微型驱动程序。 本文档的其他部分介绍了以下引用的命令和结构。

**在初始化、使用和取消初始化流式处理微型驱动程序时遵循的步骤如下**

1.  即插即用枚举器检测到微型驱动程序支持的硬件适配器。 枚举器检查注册表以解析任何符号引用，并将请求传递给 i/o 子系统。

2.  I/o 子系统将加载微型驱动程序并调用微型驱动程序的 DriverEntry 例程 [**(请) 参阅的**](/previous-versions/ff558717(v=vs.85)) **DriverEntry** 例程，其中分配和初始化了 [**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)结构。 文件对象是从 **DriverEntry** 例程中的信息创建的。

3.  然后，微型驱动程序的 **DriverEntry** 例程调用 stream 类驱动程序的 [**StreamClassRegisterMinidriver**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter) 函数并将 [**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data) 结构作为参数传递。 HW \_ 初始化 \_ 数据结构包含处理 SRBs 的微型驱动程序函数的地址。 这允许微型驱动程序响应类驱动程序发送的 SRBs。

4.  在初始化期间，stream 类驱动程序调用在 [**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data) 结构的 **HwReceivePacket** 成员中指定的函数 (参阅 [*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)) with 和 SRB，并将 **Command** 成员设置为 SRB \_ INITIALIZE \_ DEVICE。 然后，微型驱动程序初始化硬件适配器。

5.  流类驱动程序通过 SRB **HwReceivePacket** 获取流信息调用在 [**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)结构的 HwReceivePacket 成员中指定的函数 \_ \_ \_ 。 然后，微型驱动程序返回有关它所支持的流的信息。

6.  流类驱动程序使用 **HwReceivePacket** hw **\_ \_** \_ \_ [**\_ 流 \_ 对象**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object)结构调用在 hw 初始化数据结构的 HwReceivePacket 成员中使用 SRB 打开流指定的函数。 微型驱动程序执行必要的硬件操作以打开指定的流。

7.  Stream 类驱动程序通过 \_ \_ \_ \_ 向流的 HW **ReceiveDataPacket** \_ 流对象结构的 RECEIVEDATAPACKET 成员中指定的函数传递 SRB READ data 或 SRB WRITE data 命令， \_ 发送或请求流中的数据。

8.  Stream 类驱动程序通过将相应的流请求块传递 ([**hw \_ 流 \_ 请求 \_**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block) 块) 到流的 Hw 流对象结构的 **ReceiveControlPacket** 成员中指定的函数获取和设置流的属性和其他控制信息 \_ \_ 。

9.  当系统使用流时，stream 类驱动程序将使用 SRB 关闭流调用在 [**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data) 结构的 **HwReceivePacket** 成员中指定的函数 \_ \_ 。 然后，微型驱动程序将关闭指定的流。

10. 当需要对适配器进行初始化时，stream 类驱动程序将调用在 [**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data) 结构中通过 SRB 的 **HwReceivePacket** 成员指定的函数 \_ \_ 。 然后，微型驱动程序取消设备。

 

