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
ms.openlocfilehash: 4f7c9e74f958032e052a242bcd7e0c63ca1f8c6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382584"
---
# <a name="bidirectional-communication"></a>双向通信


打印子系统与打印机之间的双向打印机通信 （也称为双向通信） 是必需的打印机的自动配置。 此通信，提供与 Windows 操作系统，Windows xp 中，从开始，驱动程序和应用程序来发出请求到和从打印机设备获取响应。 自动配置基于双向通信，用户不必手动选择可安装选项，因为没有为应用程序自行配置打印机的方法。

双向通信支持涉及两个部分：

-   包含的后台处理程序 Api 的双向通信接口

-   双向通信架构的 XML 标准用于与设备交换信息

此架构描述应用程序可以对设备和请求的格式进行的请求。 后台处理程序的 Api 将请求发送到设备和还发送和接收双向数据。 应用程序还可以请求向发送网络打印提供商的网络打印机或打印机连接到远程打印机服务器。

有关如何打印后台处理程序支持双向通信的说明，请参阅[添加双向通信](adding-bidirectional-communication.md)并[后台处理程序通知](spooler-notification.md)。

## <a name="in-this-section"></a>本节内容


[双向通信架构](bidirectional-communication-schema.md)

## <a name="related-sections"></a>相关章节


[双向通信接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)

[双向通信架构参考](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)

[双向通信错误代码](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-error-codes)

 

 




