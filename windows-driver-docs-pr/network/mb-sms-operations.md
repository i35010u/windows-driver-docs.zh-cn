---
title: MB SMS 操作
description: MB SMS 操作
ms.assetid: 9a21495c-ec3d-4277-b880-dbf5b081814a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4166dc22efad9b0f99b61266647ccc0343396c91
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374013"
---
# <a name="mb-sms-operations"></a>MB SMS 操作


本主题描述的操作来配置、 读/接收、 发送和删除使用短信服务 (SMS) 功能的 MB 设备的消息。

短信支持是必需的。 微型端口驱动程序必须设置相应的发送和接收时处理它们支持的短信功能标志[OID\_WWAN\_设备\_CAPS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)查询中的请求**WwanSmsCaps**的成员[ **WWAN\_设备\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_caps)结构。 如果微型端口驱动程序不支持 SMS，它们应指定 WWAN\_短信\_CAPS\_NONE 并返回 WWAN\_状态\_SMS\_未知\_所有与 SMS 有关 Oid 的错误。

微型端口驱动程序应仅处理后的 SMS operations [OID\_WWAN\_准备\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)返回**WwanReadyStateInitialize**为设备就绪状态。 微型端口驱动程序应处理某些 SMS 操作，例如发送短信，仅在设备注册提供程序网络上 （尽管不一定是数据服务注册） 后。

MB 服务不区分不同的消息存储在设备中可用之间。 因此，微型端口驱动程序必须处理所有消息存储区和项目通过虚拟索引访问的单个虚拟消息存储区。 例如，如果设备有三个消息存储，微型端口驱动程序必须处理所有这些统称为并将其呈现作为单个消息存储到该服务。

MB 驱动程序模型支持以下短信操作：

-   SMS 配置

-   读取的 SMS

-   发送短信

-   删除 SMS

我们建议微型端口驱动程序支持 SMS 配置、 读取、 发送和删除操作，并通知用户的设备接收的任何新的 SMS 消息。

有关 SMS 的操作的详细信息，请参阅[OID\_WWAN\_SMS\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-configuration)， [OID\_WWAN\_SMS\_读取](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-read)， [OID\_WWAN\_SMS\_发送](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-send)， [OID\_WWAN\_SMS\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-delete)，和[OID\_WWAN\_SMS\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-status)。

 

 





