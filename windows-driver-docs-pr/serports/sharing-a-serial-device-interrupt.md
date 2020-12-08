---
title: 共享串行设备中断
description: 共享串行设备中断
keywords:
- COM 端口 WDK 串行设备
- 串行设备 WDK，COM 端口
- 旧 COM 端口 WDK 串行设备
- 共享串行设备中断
- 串行设备 WDK，中断
- 中断 WDK 串行设备
- 共享中断 WDK 串行设备
- 串行驱动程序 WDK，中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cc0595b3aeb99faa3cdd25cdf521efb592387ed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804935"
---
# <a name="sharing-a-serial-device-interrupt"></a>共享串行设备中断





同一多端口板上的传统 COM 端口共享单个中断。 多端口板上的 COM 端口由将端口与其相应的设备对象关联的索引或掩码标识。

独立串行设备还可以共享中断。 但是，共享中断一次只能由一个设备使用。 打开设备时，串行会将中断分配给设备。 当设备关闭时，驱动程序将释放中断以供其他设备使用。

 

 




