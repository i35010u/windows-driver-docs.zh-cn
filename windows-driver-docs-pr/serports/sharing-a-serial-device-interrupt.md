---
title: 共享串行设备中断
description: 共享串行设备中断
ms.assetid: 1d35fbc0-7031-42f3-bb22-52d2bcdcfa92
keywords:
- COM 端口 WDK 串行设备
- 串行设备 WDK、 COM 端口
- 传统的 COM 端口 WDK 串行设备
- 共享串行设备中断
- 串行设备 WDK，中断
- 中断 WDK 串行设备
- 共享的中断 WDK 串行设备
- 串行驱动程序 WDK，中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2005f1fa54d0220b6b999bde1f86691ea50255b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351822"
---
# <a name="sharing-a-serial-device-interrupt"></a>共享串行设备中断





相同的多端口板上的传统 COM 端口共享的单个中断。 通过索引或一个屏蔽，它将端口使用其相应的设备对象相关联，多端口看板上的 COM 端口进行标识。

独立串行设备还可以共享中断。 但是，共享的中断仅可通过一台设备一次。 打开设备时，序列会分配到设备的中断。 关闭设备时，该驱动程序释放由另一台设备使用的中断。

 

 




