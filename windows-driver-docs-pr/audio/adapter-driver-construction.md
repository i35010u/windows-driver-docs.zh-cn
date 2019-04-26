---
title: 适配器驱动程序构造
description: 适配器驱动程序构造
ms.assetid: e4a151b9-57aa-402f-8a0d-70547eb67917
keywords:
- 音频的微型端口驱动程序 WDK，适配器驱动程序
- 微型端口驱动程序 WDK 音频，适配器驱动程序
- 适配器驱动程序 WDK 音频，微型端口驱动程序
- 内核模式驱动程序服务 WDK 音频
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频，适配器驱动程序
- 音频适配器 WDK
- 音频适配器 WDK，构造
- 适配器驱动程序 WDK 音频，构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4490de29470544e1f15ddfca16af9849e6b2dae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325415"
---
# <a name="adapter-driver-construction"></a>适配器驱动程序构造


## <span id="adapter_driver_construction"></span><span id="ADAPTER_DRIVER_CONSTRUCTION"></span>


针对特定音频适配器卡驱动程序支持采用适配器驱动程序的形式。 适配器驱动程序由以下内容组成：

-   常规适配器代码的执行驱动程序启动和初始化，并实现所共有的适配器卡上的所有音频函数的任何操作。

-   管理适配器卡上的特定音频功能的微型端口驱动程序的一组。

硬件供应商提供的常规适配器代码和系统不提供任何微型端口驱动程序的代码。

常规适配器代码的示例，请参阅的实现**CAdapterCommon** Sb16、 Msvad 和 Ac97 示例音频驱动程序中 Microsoft Windows Driver Kit (WDK) 中的接口。

通过使用分层的方法，供应商可以编写一个适配器驱动程序，在多个级别，具体取决于适配器的硬件功能之一上运行。 在确定的给定的硬件函数要求的支持级别，供应商应首先确定是否系统提供的微型端口驱动程序已存在的支持函数 (请参阅[ **PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714)系统提供的微型端口驱动程序的函数的列表)。 如果不是，供应商必须实现专有的微型端口驱动程序，但可能仍将能够使用系统提供端口驱动程序之一 (请参阅[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)系统提供的端口的函数的列表驱动程序）。

若要实现对设备的 WDM 支持，请执行以下步骤：

1.  如果系统提供的微型端口驱动程序已支持硬件函数，使用现有的微型端口驱动程序来管理该函数。

2.  如果硬件函数与不兼容的系统提供的微型端口驱动程序，然后确定函数是否是与至少一个系统提供端口驱动程序兼容。 如果系统提供端口驱动程序支持的硬件功能，编写管理函数的微型端口驱动程序的一部分。 该微型端口驱动程序应符合所属端口驱动程序需要的微型端口接口的规范。

3.  如果没有系统提供的端口驱动程序支持的硬件功能，编写微型驱动程序以支持该函数。 微型驱动程序应符合的流式处理的类驱动程序接口规范。

本部分讨论以下主题：

[启动顺序](startup-sequence.md)

[子创建](subdevice-creation.md)

 

 




