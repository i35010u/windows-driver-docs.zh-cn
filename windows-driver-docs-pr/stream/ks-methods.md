---
title: KS 方法
description: KS 方法
ms.assetid: 1d7bd6f4-0aaf-4d77-8132-f551fd2ecbd2
keywords:
- 内核流 WDK，方法
- KS WDK，方法
- 方法 WDK 内核流式处理
- 方法设置 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 011b0614ced6082fb29b33cf6311adb6816610c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842513"
---
# <a name="ks-methods"></a>KS 方法





方法集是内核流式处理客户端可以对 KS 对象调用的一组相关的操作。 例如，分配器对象可能会提供一个方法集，其中包含分配和释放内存的方法。

微型驱动程序为其支持的每个方法集提供[**KSMETHOD\_集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmethod_set)结构。 反过来，KSMETHOD\_集结构包含一个[ **\_KSMETHOD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmethod_item)数组，该数组描述了单个方法。 微型驱动程序提供指向驱动程序提供的[*KStrMethodHandler*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkshandler)和[*KStrSupportHandler*](https://docs.microsoft.com/previous-versions/ff567206(v=vs.85))处理例程的指针，该指针位于 SupportHandler\_项结构的**MethodHandler**和**KSMETHOD**成员中。

客户端通过使用[**IOCTL\_KS\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ni-ks-ioctl_ks_method)，**通过调用** [**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)或异步 Microsoft Windows SDK 请求来发出同步方法请求。

驱动程序通过在上述调用的*InBuffer*参数中提供[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))结构来请求特定方法。

AVStream 筛选器和 pin 通过在[**KSFILTER\_说明符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构或 KSPIN 的**AutomationTable**成员中提供[**KSAUTOMATION\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksautomation_table_)结构来说明它们支持的方法[ **\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构。 有关详细信息，请参阅[定义自动化表](defining-automation-tables.md)。

 

 




