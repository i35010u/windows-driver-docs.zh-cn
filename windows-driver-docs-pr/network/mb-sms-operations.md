---
title: MB SMS 操作
description: MB SMS 操作
ms.assetid: 9a21495c-ec3d-4277-b880-dbf5b081814a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ca8ac9c17bab9d39c653de8da6fc64aedd39c6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844269"
---
# <a name="mb-sms-operations"></a>MB SMS 操作


本主题介绍使用 MB 设备的短消息服务（SMS）功能配置、读取/接收、发送和删除消息的操作。

SMS 支持是必需的。 微型端口驱动程序必须设置其支持的相应发送和接收短信功能标志，这些标志在处理[OID\_wwan\_设备](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)在 WWAN\_设备的**WwanSmsCaps**成员中\_cap 查询请求时提供支持[ **\_上限**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps)结构。 如果微型端口驱动程序不支持短信，它们应该指定 WWAN\_SMS\_CAP\_NONE，并为所有 SMS 相关的 Oid 返回 WWAN\_状态\_SMS\_未知\_错误。

小型端口驱动程序只应在 OID\_WWAN 后处理 SMS 操作[\_READY\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)返回**WwanReadyStateInitialize**作为设备就绪状态。 小型端口驱动程序应该只在设备注册到提供商网络（尽管不一定是数据服务注册）后才处理某些 SMS 操作，如发送短信。

MB 服务不区分设备中提供的不同消息存储区。 因此，微型端口驱动程序必须处理所有消息存储，并使用虚拟索引访问单个虚拟消息存储区。 例如，如果设备有三个消息存储，则微型端口驱动程序必须整体处理所有这些消息，并将它们作为单个消息存储显示到服务中。

MB 驱动程序模型支持以下 SMS 操作：

-   SMS 配置

-   阅读短信

-   发送短信

-   删除短信

建议使用微型端口驱动程序来支持 SMS 配置、读取、发送和删除操作，以及向用户通知设备收到的任何新 SMS 消息。

有关 SMS 操作的详细信息，请参阅[oid\_wwan\_sms\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-configuration)、 [oid\_WWAN\_sms\_读取](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-read)、 [oid\_wwan\_sms\_发送](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-send)， [Oid\_wwan\_sms\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-delete)和[oid\_WWAN\_sms\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-status)。

 

 





