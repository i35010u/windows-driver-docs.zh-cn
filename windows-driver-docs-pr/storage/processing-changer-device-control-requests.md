---
title: 处理更换器设备控制请求
description: 处理更换器设备控制请求
keywords:
- 转换器驱动程序，WDK 存储，请求处理
- 存储更换器驱动程序 WDK，请求处理
- IOCTLs WDK 转换器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32312758468591beb08e5d043356b991b9fafbc3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785479"
---
# <a name="processing-changer-device-control-requests"></a>处理更换器设备控制请求


## <span id="ddk_processing_changer_device_control_requests_kg"></span><span id="DDK_PROCESSING_CHANGER_DEVICE_CONTROL_REQUESTS_KG"></span>


转换器 miniclass 驱动程序不会直接处理 IOCTLs。 相反，它具有对应于由变换器类驱动程序处理的每个 IOCTL 的例程。

当类驱动程序收到请求时，它会检查参数并执行一定数量的预处理。 然后，它会调用相应的转换器 miniclass 驱动程序例程，并将指针传递到转换器设备对象和它收到的 IRP。

转换器 miniclass 驱动程序执行任何可能需要的特定于设备的验证，并生成一个或多个要发送到系统端口驱动程序的 SRBs。

如果 SRB 成功，则 miniclass 驱动程序例程会填充请求中涉及的输出参数。 无论 SRB 成功还是失败，miniclass 驱动程序例程通常都将从端口驱动程序接收的状态返回到变换器类驱动程序。

 

 




