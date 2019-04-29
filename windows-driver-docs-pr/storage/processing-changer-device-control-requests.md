---
title: 处理更换器设备控制请求
description: 处理更换器设备控制请求
ms.assetid: 3ee275c7-f2e4-47db-bd4b-db5c0c8ad399
keywords:
- 更换器驱动程序 WDK 存储，请求处理
- 存储更换器驱动程序 WDK，请求处理
- Ioctl WDK 换带机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac5f163d74cb8a014f7b914186940a799db8d0d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366278"
---
# <a name="processing-changer-device-control-requests"></a>处理更换器设备控制请求


## <span id="ddk_processing_changer_device_control_requests_kg"></span><span id="DDK_PROCESSING_CHANGER_DEVICE_CONTROL_REQUESTS_KG"></span>


换带机 miniclass 驱动程序不会直接处理 Ioctl。 相反，它具有对应于由转换器类驱动程序处理每个 IOCTL 的例程。

当类驱动程序收到请求时，它会检查参数，并执行一定的预处理。 然后，它调用的相应换带机 miniclass 驱动程序例程，将指针传递到转换器设备对象和它接收的 IRP。

换带机 miniclass 驱动程序执行任何特定于设备的验证可能要求，并生成一个或多个 Srb 将发送到系统端口驱动程序。

如果成功 SRB，miniclass 驱动程序例程填充在请求中涉及的输出参数中。 是否 SRB 成功或失败，miniclass 驱动程序例程通常返回到转换器类驱动程序收到来自端口驱动程序的状态。

 

 




