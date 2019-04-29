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
ms.openlocfilehash: fbfd0f7b38e0282710a812d60661b7532b1aebbd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380113"
---
# <a name="ks-methods"></a>KS 方法





方法集是内核流式处理客户端可以调用 KS 对象的相关操作组。 例如，一个分配器对象可以提供的方法集，其中包含分配和释放内存的方法。

微型驱动程序提供[ **KSMETHOD\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff563423)结构的每个方法将其设置支持。 接着，KSMETHOD\_集结构中包含的数组[ **KSMETHOD\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563420)描述单个方法的结构。 微型驱动程序提供驱动程序所提供的指针[ *KStrMethodHandler* ](https://msdn.microsoft.com/library/windows/hardware/ff567191)并[ *KStrSupportHandler* ](https://msdn.microsoft.com/library/windows/hardware/ff567206)处理例程中**MethodHandler**并**SupportHandler** KSMETHOD 成员\_项结构。

客户端进行同步的方法请求通过调用[ **KsSynchronousDeviceControl**](https://msdn.microsoft.com/library/windows/hardware/ff567142)，或通过调用的异步请求**DeviceIoControl** (中所述Microsoft Windows SDK 文档) 与[ **IOCTL\_KS\_方法**](https://msdn.microsoft.com/library/windows/hardware/ff560817)。

驱动程序请求特定的方法，从而[ **KSMETHOD** ](https://msdn.microsoft.com/library/windows/hardware/ff563398)结构*InBuffer*上述调用的参数。

AVStream 筛选器和插针描述它们通过提供支持的方法[ **KSAUTOMATION\_表**](https://msdn.microsoft.com/library/windows/hardware/ff560990)结构**AutomationTable**的成员任一[ **KSFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff562553)结构或[ **KSPIN\_描述符\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534)结构。 有关详细信息，请参阅[定义自动化表](defining-automation-tables.md)。

 

 




