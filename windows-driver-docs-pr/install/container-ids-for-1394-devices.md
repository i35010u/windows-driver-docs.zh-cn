---
title: 1394 设备的容器 ID
description: 1394 设备的容器 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1ec57cb541ead2c385cb3d762acd57ed0d990ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827867"
---
# <a name="container-ids-for-1394-devices"></a>1394 设备的容器 ID


1394总线规范未指定内部硬件机制，以指示设备功能是否为或不可从1394主机控制器中可移动。 Windows 附带的1394总线驱动程序将 (*devnode*) 的每个设备节点标记为从父主机控制器中可移动。

如果单个1394设备公开了多个设备功能，则会将该总线驱动程序枚举的每个 devnode 标记为可移动。 但是，Windows 附带的1394总线驱动程序识别出每个 devnode 都源自单个设备，并为每个 devnode 分配相同的容器 ID。 因此，每个1394设备接收单个设备容器对象并在 "设备和打印机" 用户界面中显示为单个设备 (UI) 。

 

 





