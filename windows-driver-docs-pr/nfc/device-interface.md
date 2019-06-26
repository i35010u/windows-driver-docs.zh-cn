---
title: NFP 设备接口
description: 客户端应用程序与通过一组定义的 I/O 控制代码发送到一个打开的句柄在邻近设备进行通信。
ms.assetid: ED63FDCF-3253-4976-8571-82F4824923C5
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 582630ac2dd4ff0f5be93f3f1d77b3c38e4c30d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377545"
---
# <a name="nfp-device-interface"></a>NFP 设备接口


客户端应用程序与通过一组定义的 I/O 控制代码发送到一个打开的句柄在邻近设备进行通信。

## <a name="publication-and-subscription-handles"></a>发布和订阅句柄


每个发布和每个订阅都表示为驱动程序的打开句柄。 因此，M 发布和 N 订阅将等同于 M + N 打开句柄驱动程序。 Windows I/O 管理器将强制实施合理的句柄计数限制的进程。

## <a name="generic-null-file-name-handles"></a>泛型 NULL 文件名称句柄


将非发布和非订阅请求发送到该驱动程序打开的通用文件句柄。 必须接受这种类型的句柄。 客户端将使用此句柄来确定最大消息大小和驱动程序的传输速率。

## <a name="ioctl-support"></a>IOCTL 支持


支持邻近设备驱动程序接口 Ioctl Nfpdev.h 中定义。 具有以下属性定义的控制代码。

-   方法\_缓冲
-   文件\_ANY\_访问
-   FILE\_DEVICE\_NFP

每个发布和每个订阅显示为其自身向驱动程序的打开句柄。 因此，M 发布和 N 订阅将等同于 M + N 打开句柄驱动程序。 Windows I/O 管理器将强制实施合理的句柄计数限制的进程。

标头 Nfpdev.h 中定义 IOCTL 代码

设备的安全描述符是保留操作系统或设备类默认值。

## <a name="reserved-and-vendor-ioctl-codes"></a>保留和供应商 IOCTL 代码


下表描述了保留和供应商特定的控件代码范围。

| 在任务栏的搜索框中键入            | 范围开始值                               | 范围结束                                 |
|-----------------|-------------------------------------------|-------------------------------------------|
| 保留        | `CTL_CODE(FILE_DEVICE_NFP, 0x0000, *, *)` | `CTL_CODE(FILE_DEVICE_NFP, 0x00FF, *, *)` |
| 特定于供应商 | `CTL_CODE(FILE_DEVICE_NFP, 0x0100, *, *)` | `CTL_CODE(FILE_DEVICE_NFP, 0x01FF, *, *)` |

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

