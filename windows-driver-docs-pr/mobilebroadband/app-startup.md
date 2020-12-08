---
title: 应用启动
description: 应用启动
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cd661490cf25abcf4c80b80856922cc9aa8b32a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782529"
---
# <a name="app-startup"></a>应用启动


当移动宽带应用启动时，它应检查 Internet 访问是否可用。 应用可以使用 API 来发现各种 Internet 连接状态。 然后，该应用程序可以确定在 Internet 连接处于 "围墙园" 状态时它是否可以访问后端数据。 如果没有 Internet 连接，应用应向用户显示相应的消息或脱机体验。

如果将多个操作员的订户标识模块 (Sim) 附加到电脑，则应用可以确定这一点。 应用必须提供适用于多个连接的操作员设备或帐户的用户界面。

例如，应用可以从移动宽带设备读取 IMSI 和 IMEI 信息。 此信息可用作身份验证方案的一部分，以及用于将用户名和密码信息发送到后端的登录屏幕。 Windows 提供了一个 API，用于安全地存储用户名和密码信息，应用程序随后可以在第一次登录尝试后用于身份验证。 必须通过安全 HTTP (HTTPS) 与操作员后端交换所有用户名和密码信息。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带应用方案](./account-management.md)

 

