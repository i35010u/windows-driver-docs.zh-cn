---
title: 应用启动
description: 应用启动
ms.assetid: 0aca0d3c-9865-4a11-a9c5-e77cc735ba21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3fe25da46f1c4222ca279e66218f9811a934262
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351319"
---
# <a name="app-startup"></a>应用启动


移动宽带应用启动时，它应检查是否都可以访问 Internet。 应用可以使用一个 API 来发现 Internet 连接的各种状态。 然后，应用程序可以确定是否连接到互联网处于"围墙的花园"状态时，它可以访问后端数据。 如果没有 Internet 连接，应用应该向用户显示相应的消息或脱机的体验。

如果多个运算符的订阅服务器上标识模块 (Sim) 连接到 PC 中，应用程序可以确定此大小。 应用程序必须提供适用于多个运算符连接的设备或帐户的用户界面。

例如，应用可以从移动宽带设备读取的 IMSI 和 IMEI 信息。 除了或取代将用户名和密码信息发送到后端的登录屏幕上，此信息可以用作身份验证方案的一部分。 Windows 提供了一个 API，用于安全地存储应用程序可以随后使用后首次登录尝试的身份验证的用户名和密码信息。 所有的用户名和密码信息必须通过安全 HTTP (HTTPS) 交换运算符后端使用。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带应用方案](mobile-broadband-app-scenarios.md)

 

 






