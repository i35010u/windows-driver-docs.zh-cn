---
title: 智能卡读卡器驱动程序中的 IOCTL 请求管理
description: 智能卡读卡器驱动程序中的 IOCTL 请求管理
keywords:
- 智能卡驱动程序 WDK，IOCTL 请求管理
- IOCTLs WDK 智能卡
- 供应商提供的驱动程序 WDK 智能卡，IOCTL 请求管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d44ce87c273abb3f82abd660946e4edf2cbd9eda
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811911"
---
# <a name="management-of-ioctl-requests-in-a-smart-card-reader-driver"></a>智能卡读卡器驱动程序中的 IOCTL 请求管理


## <span id="_ntovr_management_of_ioctl_requests_in_a_smart_card_reader_driver"></span><span id="_NTOVR_MANAGEMENT_OF_IOCTL_REQUESTS_IN_A_SMART_CARD_READER_DRIVER"></span>


IOCTL 请求的管理在智能卡驱动程序库中居中。 大多数情况下，智能卡读卡器驱动程序只需将 IOCTL 请求传递到 [**SmartcardDeviceControl (WDM)**](/previous-versions/ff548939(v=vs.85)) 库例程。

不过，智能卡驱动程序库所服务的一组标准 IOCTL 请求并不一定足以完全支持读取器设备的功能。 因此，供应商可能需要创建自己的 IOCTL 请求。 此外，某些标准 IOCTL 请求可能需要在由驱动程序库处理后进行其他处理。 出于这两个原因，使用智能卡读卡器的驱动程序体系结构，供应商提供的读卡器驱动程序可以实现一系列回调例程。 这些回调例程在需要时提供进一步的 IOCTLs 处理。

以下各节介绍了读取器驱动程序如何管理 IOCTL 请求、回调例程机制的工作方式，以及读取器驱动程序必须执行哪些操作来初始化其回调例程。

具体而言，包括以下主题：

[与智能卡驱动程序库的交互](interaction-with-the-smart-card-driver-library.md)

[智能卡驱动程序库回调例程](smart-card-driver-library-callback-routines.md)

[智能卡回调参数](smart-card-callback-parameters.md)

 

