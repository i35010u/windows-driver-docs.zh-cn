---
title: 电池设备设计指南
description: 电池设备设计指南
ms.assetid: d8eecfcb-6c06-40d1-8c78-b8c88eb890f2
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: cdc798165ed99ba241f2f9ea10d26f4c2f71c5ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328444"
---
# <a name="battery-devices-design-guide"></a>电池设备设计指南


## <span id="ddk_design_guide_battery_devices_dg"></span><span id="DDK_DESIGN_GUIDE_BATTERY_DEVICES_DG"></span>


电池通常有一对驱动程序：Microsoft 提供的通用电池类驱动程序，以及专门为具体电池类型编写的小型驱动程序。

类驱动程序定义系统中电池的整体功能，并与电源管理器进行交互。

此设计指南重点介绍了[编写电池微型类驱动程序](writing-battery-miniclass-drivers.md)。

此外，本部分还包括了有关[编写用于旧版 Windows 的UPS 微型驱动程序](writing-ups-minidrivers.md)的信息。

 

 




