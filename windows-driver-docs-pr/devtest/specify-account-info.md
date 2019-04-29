---
title: 在移动宽带元数据创作向导中指定帐户信息
description: 在移动宽带元数据创作向导中指定帐户信息
ms.assetid: FFE19760-360F-482C-BBD8-7068D2DD34E5
keywords:
- 在移动宽带元数据创作向导中指定帐户信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cbd84da67bdcfc55a60463002a23e1cead8768e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358923"
---
# <a name="specify-account-information-in-the-mobile-broadband-metadata-authoring-wizard"></a>在移动宽带元数据创作向导中指定帐户信息


若要指定你的移动宽带帐户信息，请填写以下可选字段上**帐户**选项卡：

-   下一步**购买的配置文件**，单击**浏览**，然后选择基于定义的 APN 连接到以完成计划的购买 WWAN v2 配置文件架构的配置文件的用户选择。

    **购买配置文件**用于建立连接受到限制，以使最终用户可以购买新的订阅。 用于所有订阅服务器具有只有一个采购 APN GSM 运算符可用于移动宽带服务元数据提供的到 PC。 如果有多个采购 APNs，不要指定此处购买配置文件。 相反，使用 APN 数据库或帐户预配元数据设置适当的采购 APN。

-   下一步**Internet 配置文件**，单击**浏览**，然后选择基于定义的 APN 连接到 Internet 的 WWAN v2 配置文件架构的配置文件。

    **Internet 配置文件**使用的连接管理器，从而自动连接到网络。 每个移动宽带订阅可以有一个用于连接到家庭网络运算符的默认配置文件。 GSM 运算符具有只有一个 Internet 配置文件用于所有订阅服务器可以使用移动宽带服务元数据提供到 PC。 如果有多个采购 APNs，不要指定此处 Internet 配置文件。 相反，使用 APN 数据库或帐户预配元数据设置适当的 Internet APN。

    有关更详细的移动宽带的配置文件架构的信息，请参阅[服务的元数据包架构引用适用于 Windows 8 的](https://go.microsoft.com/fwlink/p/?LinkId=226755)。

-   下一步**PIN 解锁函数**，选择**上移动宽带 sims 就允许标准用户执行 PIN 解锁**若要启用标准用户执行 PIN 解锁上为其移动宽带 SIMs 函数应用服务。

    详细了解 PIN 解锁，请参阅[概述的移动宽带 Windows 8 中](https://go.microsoft.com/fwlink/p/?LinkId=242052)。

-   下**受信任的证书**，填写**主题**并**颁发者**字段。 此信息来自使用元数据程序包进行签名的证书。

    （如果不使用 web 浏览器基于的 XML 预配，则可以跳过此步骤。）

    在初始设置过程，从移动网络运营商的 web 页或强制网络门户传递哈希值用于验证数字签名设置文件中的受信任的证书。 此项支持的方案，其中用户购买该服务之前安装的移动宽带应用。 这两个字段的格式应为可分辨名称，并且必须匹配**使用者**并**颁发者**使用采购网站上的预配文件进行签名的数字证书的字段。 有关可分辨名称的详细信息，请参阅部分中的 RFC 4514[字符串表示形式的可分辨名称 Internet 工程任务组网站上](https://go.microsoft.com/fwlink/p/?LinkId=242261)。

    有关预配的详细信息，请参阅[服务的元数据包架构引用适用于 Windows 8 的](https://go.microsoft.com/fwlink/p/?LinkId=226755)。

 

 





