---
title: 启动串行设备
description: 启动串行设备
ms.assetid: 83f86da6-0acb-4cad-8856-e826c98c2182
keywords:
- 串行驱动程序 WDK，设备电源
- 启动串行设备 WDK
- 打开串行设备 WDK
- 串行设备 WDK，启动
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6404d63faa250bda51ccd808b5f4cc6bec08fc5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331112"
---
# <a name="powering-up-a-serial-device"></a>启动串行设备





必须打开串行设备 (设备电源状态**PowerDeviceD0**) 用于 Serial 与设备硬件进行通信。 如果设备未启用，则序列将尝试打开设备驱动程序完成请求之前。

 

 




