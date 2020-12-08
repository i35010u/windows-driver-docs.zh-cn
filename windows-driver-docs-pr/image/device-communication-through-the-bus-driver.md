---
title: 通过总线驱动程序进行的设备通信
description: 通过总线驱动程序进行的设备通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de7140b5b1225dd22e6bd7bca4b324ce0fbb52c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792879"
---
# <a name="device-communication-through-the-bus-driver"></a>通过总线驱动程序进行的设备通信





WIA 微型驱动程序的主要职责是与设备进行通信。 当 WIA 应用程序调用 WIA 服务时，该请求将通过 [IStiUSD](istiusd-com-interface.md) 或 [IWiaMiniDrv](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv) 接口转发到 wia 微型驱动程序的接口。 在某些情况下，WIA 微型驱动程序必须查询物理设备或在设备上执行其他操作。 微型驱动程序的设备通信层负责将请求从 WIA 服务转换为设备可以理解的请求，然后通过总线驱动程序堆栈将请求发送到设备。 同样，当设备将其响应备份到总线驱动程序堆栈时，设备通信层负责将设备响应转换为 WIA 服务理解的响应。

与总线驱动程序堆栈的所有通信都是通过调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile** 和 **DeviceIoControl** 函数来执行的，如 Microsoft Windows SDK 文档中所述。 有关与总线驱动程序堆栈通信的详细信息，请参阅 [访问静止图像设备 Kernel-Mode 驱动程序](accessing-kernel-mode-drivers-for-still-image-devices.md)。

 

