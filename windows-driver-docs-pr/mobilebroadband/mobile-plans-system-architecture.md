---
title: 移动计划系统体系结构
description: 移动计划系统体系结构
keywords:
- Windows Mobile 计划移动运营商
ms.date: 07/31/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 5ce7e7f12e1486c1ab76e00d7ee8412ff29e56ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832939"
---
# <a name="mobile-plans-system-architecture"></a>移动计划系统体系结构

此页概述了移动计划系统体系结构的主要组件。 它们共同构成了移动计划计划。 并非每个移动运营商部署都需要此处列出的每个组件。

移动计划系统体系结构由以下5个主要组件构成：

### <a name="mobile-plans-app"></a>移动计划应用

这是由 Microsoft 在所有启用了手机网络的 Windows 10 设备上预安装的通用 Windows 平台 (UWP) 应用。 移动计划应用是在用户的设备上运行的用于托管最终用户体验的主要客户端环境。 移动计划应用还可以在后台运行，以触发某些事件 (例如显示 toast 通知) 。

### <a name="mobile-plans-service"></a>移动计划服务

移动计划服务是基于云的服务层，它向移动计划应用提供数据。 它还向移动运营商 API 提供经过身份验证的接口。

### <a name="mobile-operator-web-portal"></a>移动运营商 Web 门户

这是由移动运营商托管的基于 web 的运行时环境。 用户通过 web 导航体验移动运营商 web 门户，并在移动计划应用的原位中呈现。

### <a name="mobile-operator-api"></a>移动运营商 API

这是由移动运营商托管的编程接口，用于向移动计划公开用户数据，这些数据可在运行时提取，以更新向用户显示的内容。 在运行时提取的用户数据的一个示例是用户的预付余额。

### <a name="mobile-operator-sm-dp"></a>移动运营商 SM-DP +

此服务负责创建移动运营商的 eSIM 配置文件并将其传送到 Windows 10 设备。

## <a name="functional-overview"></a>功能概述

下图显示了有关如何在典型流中使用上述组件来成功激活订阅和安装 eSIM 配置文件的高级概述。 请注意，其他流也是可以实现的。

![移动计划系统体系结构](images/mobile_plans_system_architecture.png)

1. 移动计划应用在 Windows 10 设备上启动，并从移动计划服务中检索基本的功能数据。
2. 移动计划应用程序调用移动运营商 web 门户，并传递相关参数，门户可使用这些参数确定要显示的用户体验。
3. 移动运营商 web 门户中的激活流完成后，移动运营商从 SM + 服务器请求 eSIM 配置文件。 相应的 eSIM 激活代码将返回到移动运营商 web 门户。
4. 移动运营商 web 门户将 eSIM 配置文件激活代码返回到移动计划应用。
5. 移动计划应用将激活代码传递到 Windows LPA，后者联系 SM + 服务器来检索 eSIM 配置文件。
6. ESIM 配置文件会下载并安装到 Windows 10 设备 eSIM，并已激活。 激活后，Windows 10 设备将注册到移动运营商网络上。
7. 用户打开 Windows 网络弹出窗口，它调用移动计划服务的请求以获取可用余额。
8. 移动计划服务向移动运营商 API 发出 Get 余额请求，此操作返回向用户显示的可用余额。
