---
title: KS 方法
description: KS 方法
ms.assetid: 1d7bd6f4-0aaf-4d77-8132-f551fd2ecbd2
keywords:
- 流式处理 WDK，方法的内核
- KS WDK 方法
- 流式处理的方法 WDK 内核
- 方法设置 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b78f53f79834bf8f01d5e0b847fbd260d69bfd8c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382514"
---
# <a name="ks-methods"></a>KS 方法





方法集是内核流式处理客户端可以调用 KS 对象的相关操作组。 例如，一个分配器对象可以提供的方法集，其中包含分配和释放内存的方法。

微型驱动程序提供[ **KSMETHOD\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmethod_set)结构的每个方法将其设置支持。 接着，KSMETHOD\_集结构中包含的数组[ **KSMETHOD\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmethod_item)描述单个方法的结构。 微型驱动程序提供驱动程序所提供的指针[ *KStrMethodHandler* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkshandler)并[ *KStrSupportHandler* ](https://docs.microsoft.com/previous-versions/ff567206(v=vs.85))处理例程中**MethodHandler**并**SupportHandler** KSMETHOD 成员\_项结构。

客户端进行同步的方法请求通过调用[ **KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)，或通过调用的异步请求**DeviceIoControl** (中所述Microsoft Windows SDK 文档) 与[ **IOCTL\_KS\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ni-ks-ioctl_ks_method)。

驱动程序请求特定的方法，从而[ **KSMETHOD** ](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))结构*InBuffer*上述调用的参数。

AVStream 筛选器和插针描述它们通过提供支持的方法[ **KSAUTOMATION\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksautomation_table_)结构**AutomationTable**的成员任一[ **KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)结构或[ **KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。 有关详细信息，请参阅[定义自动化表](defining-automation-tables.md)。

 

 




