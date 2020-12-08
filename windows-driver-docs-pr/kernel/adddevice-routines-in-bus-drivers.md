---
title: 总线驱动程序中的 AddDevice 例程
description: 总线驱动程序中的 AddDevice 例程
keywords:
- 总线驱动程序 WDK 内核
- AddDevice 例程 WDK 内核，总线驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94c2a1c6eaa3b5f85ac07261a8f1c04dfe96a2ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787325"
---
# <a name="adddevice-routines-in-bus-drivers"></a>总线驱动程序中的 AddDevice 例程





PnP 总线驱动程序具有 *AddDevice* 例程，但当总线驱动程序充当其控制器或适配器的函数驱动程序时，将调用该驱动程序。 例如，PnP 管理器调用 USB 集线器总线驱动程序的 *AddDevice* 例程来添加集线器设备。 不会为插入到中心)  (设备的中心的子集线器调用集线器驱动程序的 *AddDevice* 例程。

 

 




