---
title: 1394 设备的容器 ID
description: 1394 设备的容器 ID
ms.assetid: 667df2c6-bbbd-41da-b626-da493e316016
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1ef0e397ed3eb916529c8623d795dc3d1f20dfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346853"
---
# <a name="container-ids-for-1394-devices"></a>1394 设备的容器 ID


1394 总线规范不会指定一个内部硬件的机制来指示设备函数是还是不能删除从 1394年主控制器。 Windows 附带的 1394年总线驱动程序将标记每个设备节点 (*devnode*) 从父主机控制器为可移动。

如果在单个的 1394年设备公开多个设备函数，总线驱动程序枚举每个 devnode 标记为可移动。 但是，Windows 附带的 1394年总线驱动程序识别每个 devnode 源自单个设备，并将相同的容器 ID 分配给每个 devnode。 因此，每个 1394年设备接收单个设备容器对象，并显示为单个设备的设备和打印机用户界面 (UI) 中。

 

 





