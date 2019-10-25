---
title: 通过总线驱动程序进行的设备通信
description: 通过总线驱动程序进行的设备通信
ms.assetid: 093e95db-dc3e-467b-9163-e61d793c042e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 909f8ab2875e2c70557214b3ce8cf3f3d03bd0aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840856"
---
# <a name="device-communication-through-the-bus-driver"></a>通过总线驱动程序进行的设备通信





WIA 微型驱动程序的主要职责是与设备进行通信。 当 WIA 应用程序调用 WIA 服务时，该请求将通过[IStiUSD](istiusd-com-interface.md)或[IWiaMiniDrv](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)接口转发到 wia 微型驱动程序的接口。 在某些情况下，WIA 微型驱动程序必须查询物理设备或在设备上执行其他操作。 微型驱动程序的设备通信层负责将请求从 WIA 服务转换为设备可以理解的请求，然后通过总线驱动程序堆栈将请求发送到设备。 同样，当设备将其响应备份到总线驱动程序堆栈时，设备通信层负责将设备响应转换为 WIA 服务理解的响应。

与总线驱动程序堆栈的所有通信都是通过调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile**和**DeviceIoControl**函数来执行的，如 Microsoft Windows SDK 文档中所述。 有关与总线驱动程序堆栈通信的详细信息，请参阅[访问静止图像设备的内核模式驱动程序](accessing-kernel-mode-drivers-for-still-image-devices.md)。

 

 




