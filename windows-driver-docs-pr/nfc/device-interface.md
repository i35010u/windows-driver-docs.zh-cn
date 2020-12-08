---
title: NFP 设备接口
description: 客户端应用程序通过一组发送到打开句柄的 i/o 控制代码来与邻近感应设备通信。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32f58c86eac5f7aa303dfc8801207a6fcc3688d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813595"
---
# <a name="nfp-device-interface"></a>NFP 设备接口


客户端应用程序通过一组发送到打开句柄的 i/o 控制代码来与邻近感应设备通信。

## <a name="publication-and-subscription-handles"></a>发布和订阅句柄


每个发布和每个订阅都表示为驱动程序的打开句柄。 因此，M 发布和 N 订阅将等同于 M + N 打开驱动程序的句柄。 Windows i/o 管理器将在进程上强制实施合理的句柄计数限制。

## <a name="generic-null-file-name-handles"></a>一般空文件名句柄


打开泛型文件句柄，以便向驱动程序发送非发布和非订阅请求。 必须接受此类型的句柄。 客户端将使用此句柄来确定最大消息大小和驱动程序的传输速率。

## <a name="ioctl-support"></a>IOCTL 支持


支持邻近设备驱动程序接口的 IOCTLs 在 Nfpdev 中定义。 控制代码是用以下属性定义的。

-   方法 \_ 缓冲
-   文件 \_ 任何 \_ 访问权限
-   文件 \_ 设备 \_ NFP

每个发布和每个订阅均表现为驱动程序的打开句柄。 因此，M 发布和 N 订阅将等同于 M + N 打开驱动程序的句柄。 Windows i/o 管理器将在进程上强制实施合理的句柄计数限制。

IOCTL 代码在标头 Nfpdev 中定义

设备的安全描述符将保留为 OS 或设备类默认值。

## <a name="reserved-and-vendor-ioctl-codes"></a>保留和供应商 IOCTL 代码


下表介绍了保留的和供应商的特定控制代码范围。

| 类型            | 范围开始                               | 范围结束                                 |
|-----------------|-------------------------------------------|-------------------------------------------|
| 预留        | `CTL_CODE(FILE_DEVICE_NFP, 0x0000, *, *)` | `CTL_CODE(FILE_DEVICE_NFP, 0x00FF, *, *)` |
| 特定于供应商 | `CTL_CODE(FILE_DEVICE_NFP, 0x0100, *, *)` | `CTL_CODE(FILE_DEVICE_NFP, 0x01FF, *, *)` |

 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)
