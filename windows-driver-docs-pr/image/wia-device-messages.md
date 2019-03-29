---
title: WIA 设备消息
description: WIA 设备消息
ms.assetid: b498a75d-1252-4f13-ae62-9a53491c2bde
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d27a47b4988e4168f9f0e20685a0b4275599ebe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575314"
---
# <a name="wia-device-messages"></a>WIA 设备消息


以下列表显示所有当前定义的 WIA 设备消息。 可以将这些消息发送期间**IWiaTransfer::Download**并**IWiaTransfer::Upload**。 **IWiaTransfer** Microsoft Windows SDK 文档中详细介绍了接口。

### <a name="device-status-messages"></a>设备的状态消息：

-   WIA\_状态\_WARMING\_向上

-   WIA\_状态\_校准

-   WIA\_STATUS\_RESERVING\_NETWORK\_DEVICE

-   WIA\_STATUS\_NETWORK\_DEVICE\_RESERVED

-   WIA\_状态\_清除

### <a name="device-error-messages"></a>设备的错误消息：

-   WIA\_ERROR\_GENERAL\_ERROR

-   WIA\_ERROR\_PAPER\_JAM

-   WIA\_错误\_纸张\_空

-   WIA\_错误\_纸张\_问题

-   WIA\_错误\_脱机

-   WIA\_错误\_忙

-   WIA\_错误\_WARMING\_向上

-   WIA\_错误\_用户\_干预

-   WIA\_ERROR\_ITEM\_DELETED

-   WIA\_错误\_设备\_通信

-   WIA\_错误\_无效\_命令

-   WIA\_错误\_不正确\_硬件\_设置

-   WIA\_错误\_设备\_已锁定

-   WIA\_错误\_异常\_IN\_驱动程序

-   WIA\_错误\_无效\_驱动程序\_响应

-   WIA\_错误\_涵盖\_打开

-   WIA\_错误\_LAMP\_OFF

-   WIA\_错误\_目标

-   WIA\_ERROR\_NETWORK\_RESERVATION\_FAILED

WIA 默认错误处理程序

目前，WIA 默认错误处理程序支持以下设备的消息：

-   WIA\_状态\_WARMING\_向上

-   WIA\_状态\_校准

-   WIA\_STATUS\_RESERVING\_NETWORK\_DEVICE

-   WIA\_STATUS\_NETWORK\_DEVICE\_RESERVED

-   WIA\_ERROR\_PAPER\_JAM

-   WIA\_错误\_设备\_已锁定

-   WIA\_ERROR\_NETWORK\_RESERVATION\_FAILED

-   WIA\_错误\_涵盖\_打开

-   WIA\_错误\_LAMP\_OFF

-   WIA\_错误\_目标

-   WIA\_错误\_纸张\_空

 

 




