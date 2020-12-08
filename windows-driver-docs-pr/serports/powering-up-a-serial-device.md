---
title: 启动串行设备
description: 启动串行设备
keywords:
- 串行驱动程序 WDK，设备电源
- 打开串行设备 WDK
- 打开串行设备 WDK
- 串行设备 WDK，通电
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec350ec7c85c8c899da0ff6563c1dea78af9d04
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805001"
---
# <a name="powering-up-a-serial-device"></a>启动串行设备





串行设备必须在设备电源状态 **PowerDeviceD0** 中打开 () ，以便串行与设备硬件通信。 如果设备未打开，则串行将尝试在驱动程序完成请求之前打开设备。

 

 




