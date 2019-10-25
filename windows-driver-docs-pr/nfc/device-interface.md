---
title: NFP 设备接口
description: 客户端应用程序通过一组发送到打开句柄的 i/o 控制代码来与邻近感应设备通信。
ms.assetid: ED63FDCF-3253-4976-8571-82F4824923C5
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a764b889eb57c3be72d78c5a0365b1110a0978df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842538"
---
# <a name="nfp-device-interface"></a>NFP 设备接口


客户端应用程序通过一组发送到打开句柄的 i/o 控制代码来与邻近感应设备通信。

## <a name="publication-and-subscription-handles"></a>发布和订阅句柄


每个发布和每个订阅都表示为驱动程序的打开句柄。 因此，M 发布和 N 订阅将等同于 M + N 打开驱动程序的句柄。 Windows i/o 管理器将在进程上强制实施合理的句柄计数限制。

## <a name="generic-null-file-name-handles"></a>一般空文件名句柄


打开泛型文件句柄，以便向驱动程序发送非发布和非订阅请求。 必须接受此类型的句柄。 客户端将使用此句柄来确定最大消息大小和驱动程序的传输速率。

## <a name="ioctl-support"></a>IOCTL 支持


支持邻近设备驱动程序接口的 IOCTLs 在 Nfpdev 中定义。 控制代码是用以下属性定义的。

-   \_缓冲的方法
-   文件\_任何\_访问
-   文件\_设备\_NFP

每个发布和每个订阅均表现为驱动程序的打开句柄。 因此，M 发布和 N 订阅将等同于 M + N 打开驱动程序的句柄。 Windows i/o 管理器将在进程上强制实施合理的句柄计数限制。

IOCTL 代码在标头 Nfpdev 中定义

设备的安全描述符将保留为 OS 或设备类默认值。

## <a name="reserved-and-vendor-ioctl-codes"></a>保留和供应商 IOCTL 代码


下表介绍了保留的和供应商的特定控制代码范围。

| 在任务栏的搜索框中键入            | 范围开始                               | 范围结束                                 |
|-----------------|-------------------------------------------|-------------------------------------------|
| 保留        | `CTL_CODE(FILE_DEVICE_NFP, 0x0000, *, *)` | `CTL_CODE(FILE_DEVICE_NFP, 0x00FF, *, *)` |
| 特定于供应商 | `CTL_CODE(FILE_DEVICE_NFP, 0x0100, *, *)` | `CTL_CODE(FILE_DEVICE_NFP, 0x01FF, *, *)` |

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

