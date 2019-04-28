---
title: 智能卡读卡器驱动程序中的 IOCTL 请求管理
description: 智能卡读卡器驱动程序中的 IOCTL 请求管理
ms.assetid: 610476fc-59e7-4981-9afa-20ed7cc697c1
keywords:
- 智能卡驱动程序 WDK，IOCTL 请求管理
- Ioctl WDK 智能卡
- 供应商提供的驱动程序 WDK 的智能卡，IOCTL 请求管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c6a1f254bda1ac3754f278461600b929592a69a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331107"
---
# <a name="management-of-ioctl-requests-in-a-smart-card-reader-driver"></a>智能卡读卡器驱动程序中的 IOCTL 请求管理


## <span id="_ntovr_management_of_ioctl_requests_in_a_smart_card_reader_driver"></span><span id="_NTOVR_MANAGEMENT_OF_IOCTL_REQUESTS_IN_A_SMART_CARD_READER_DRIVER"></span>


IOCTL 请求管理智能卡驱动程序库中居中。 大多数情况下，智能卡读卡器驱动程序可以只需 IOCTL 将请求传递到[ **SmartcardDeviceControl (WDM)** ](https://msdn.microsoft.com/library/windows/hardware/ff548939)库例程。

但是，提供服务的智能卡驱动程序库 IOCTL 请求的标准集并不总是不足以完全支持的读取器设备的功能。 因此，供应商可能需要创建其自己 IOCTL 请求。 此外，某些标准 IOCTL 请求可能需要额外的处理之后由驱动程序库处理。 对于这两个原因，通过驱动程序的智能卡读取器供应商提供读卡器驱动程序体系结构可以实现一系列的回调例程。 这些回调例程提供 Ioctl 时所需的进一步处理。

以下部分介绍如何读卡器驱动程序管理 IOCTL 请求、 回调例程机制的工作原理，以及读卡器驱动程序必须做什么来初始化其回调例程。

具体而言，包括以下主题：

[与智能卡驱动程序库的交互](interaction-with-the-smart-card-driver-library.md)

[智能卡驱动程序库回调例程](smart-card-driver-library-callback-routines.md)

[智能卡回调参数](smart-card-callback-parameters.md)

 

 





