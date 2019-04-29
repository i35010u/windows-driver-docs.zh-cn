---
title: 获取有关并行端口的信息
description: 获取有关并行端口的信息
ms.assetid: d8ae2296-05b6-419a-93cc-00fcb12d41fe
keywords:
- 并行端口 WDK，获取信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7754095795119f3061223b0fb0f1bf2c1c03831c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373539"
---
# <a name="obtaining-information-about-a-parallel-port"></a>获取有关并行端口的信息





客户端使用的并行端口之前，它可以获取有关以下信息：

-   并行端口使用的资源

-   硬件功能的并行端口

-   [并行端口回调例程](https://msdn.microsoft.com/library/windows/hardware/ff544307)，可以使用的内核模式驱动程序

客户端使用以下内置设备控制请求获取上面的信息：

[**IOCTL\_INTERNAL\_GET\_PARALLEL\_PORT\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff544002)

[**IOCTL\_内部\_获取\_详细\_并行\_端口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff543996)

[**IOCTL\_INTERNAL\_GET\_PARALLEL\_PNP\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff543997)

客户端通过使用版本并行端口的信息[ **IOCTL\_内部\_发行\_并行\_端口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff544047)请求。

 

 




