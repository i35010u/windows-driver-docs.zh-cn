---
title: WDI NDIS 空闲检测
description: 下图显示了 NDIS 空闲检测的简单状态图，它用于驱动 USB 选择性挂起。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8fe760cbea42d0db96839f4572ec09be4f7634e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821225"
---
# <a name="wdi-ndis-idle-detection"></a>WDI NDIS 空闲检测


下图显示了 NDIS 空闲检测的简单状态图，它用于驱动 USB 选择性挂起。

![wdi 用于 usb 选择性挂起的 ndis 空闲检测](images/wdi-idle-detection-selective-suspend.png)

如果 WDI 设备/驱动程序支持 USB 选择性挂起，NDIS 将检测其空闲状态以将设备发送到低功耗状态 (D2) 。

 

 





