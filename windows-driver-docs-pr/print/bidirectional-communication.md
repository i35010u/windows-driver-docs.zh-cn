---
title: 双向通信
description: 双向通信
ms.assetid: c88f5f43-4a14-4f63-9f17-b6680fc0d645
keywords:
- 打印机配置 WDK，双向通信
- 双向通信 WDK 打印
- 双向通信 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07d32ba37ae42ee73e2999d15b25e34abaef7a91
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218268"
---
# <a name="bidirectional-communication"></a>双向通信


双向打印机通信 (也称为在打印子系统和打印机之间进行双向通信) 对于打印机的自动配置非常重要。 从 Windows XP 开始，与 Windows 操作系统一起提供的这种通信使驱动程序和应用程序能够向打印机设备发出请求并获得响应。 使用基于双向通信的自动配置，用户不必手动选择可安装的选项，因为有一种方法可以让应用程序自行配置打印机。

双向通信支持包括两个部分：

-   双向通信接口，包括后台处理程序 Api

-   双向通信架构，一种用于与设备交换信息的 XML 标准

此架构描述了应用程序可以对设备进行的请求以及请求的格式。 后台处理程序 Api 将请求发送到设备，同时发送和接收双向数据。 应用程序还可以将请求发送到网络打印机或连接到远程打印机服务器的打印机的网络打印提供程序。

有关打印后台处理程序如何支持双向通信的说明，请参阅 [添加双向通信](adding-bidirectional-communication.md) 和 [后台处理程序通知](spooler-notification.md)。

## <a name="in-this-section"></a>本节内容


[双向通信架构](bidirectional-communication-schema.md)

## <a name="related-sections"></a>相关章节


[双向通信接口](/windows-hardware/drivers/ddi/_print/index)

[双向通信架构参考](./bidi-communications-schema-reference.md)

[双向通信错误代码](./bidi-error-codes.md)

 

