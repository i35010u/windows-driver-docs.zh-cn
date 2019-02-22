---
title: AddDevice 总线驱动程序中的例程
description: AddDevice 总线驱动程序中的例程
ms.assetid: 70af7116-2f29-4d77-a6d5-c1e0417e6f81
keywords:
- 总线驱动程序 WDK 内核
- AddDevice 例程 WDK 内核，总线驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1319496fd8c4bde1840c9ece931223f1ed1d85ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522913"
---
# <a name="adddevice-routines-in-bus-drivers"></a>AddDevice 总线驱动程序中的例程





即插即用总线驱动程序包含*AddDevice*例程，但它名为当总线驱动程序充当其控制器或适配器功能驱动程序。 例如，即插即用管理器调用 USB 集线器总线驱动程序*AddDevice*例程，以添加 hub 设备。 在中心驱动程序*AddDevice*例程不会调用针对的中心 （插入到中心的设备） 的子级。

 

 




