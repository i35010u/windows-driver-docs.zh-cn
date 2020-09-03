---
title: 在移动宽带元数据创作向导中指定帐户信息
description: 在移动宽带元数据创作向导中指定帐户信息
ms.assetid: FFE19760-360F-482C-BBD8-7068D2DD34E5
keywords:
- 在移动宽带元数据创作向导中指定帐户信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 760bfee1b360bc68c43573aee0f5785e3386bab9
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384321"
---
# <a name="specify-account-information-in-the-mobile-broadband-metadata-authoring-wizard"></a>在移动宽带元数据创作向导中指定帐户信息


若要指定移动宽带帐户信息，请在 " **帐户** " 选项卡上填写以下可选字段：

-   在 " **购买配置文件**" 旁边，单击 " **浏览**"，然后选择基于 WWAN v2 配置文件架构的配置文件，该架构定义要连接到哪些 APN 才能完成用户选择的计划的购买。

    **购买配置文件** 用于建立有限的连接性，使最终用户能够购买新的订阅。 对于所有订阅者只有一个购买 APN 的 GSM 操作员，可以使用移动宽带服务元数据将其提供给 PC。 如果有多个购买 APNs，请不要在此处指定购买配置文件。 相反，请使用 APN 数据库或帐户预配元数据来设置相应的购买接入点。

-   在 " **Internet 配置文件**" 旁边，单击 " **浏览**"，然后根据 WWAN v2 配置文件架构（定义要连接到 Internet 的 APN）选择配置文件。

    **Internet 配置文件** 由连接管理器用来自动连接到网络。 每个移动宽带订阅可以有一个用于连接到家庭网络操作员的默认配置文件。 对于所有订阅者只有一个 Internet 配置文件的 GSM 操作员，可以使用移动宽带服务元数据将其提供给 PC。 如果有多个购买 APNs，请不要在此指定 Internet 配置文件。 相反，请使用 APN 数据库或帐户预配元数据来设置适当的 Internet 接入点。

    有关移动宽带配置文件架构的详细信息，请参阅 [服务元数据包架构参考](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/service-metadata-package-schema-reference)。

-   在 "锁定 **解锁函数**" 旁边，选择 " **允许标准用户对移动宽带 sim 执行 pin 解锁** "，以使标准用户能够在其移动宽带 sim 上为服务执行 pin 解锁功能。

    有关 PIN 解锁的详细信息，请参阅 [解锁设备](../mobilebroadband/unlock-a-device.md)。

-   在 " **受信任的证书**" 下填写 " **使用者** " 和 " **颁发者** " 字段。 此信息来自用于对元数据包进行签名的证书。

     (如果未使用基于 web 浏览器的 XML 预配，则可以跳过此步骤。 ) 

    受信任的证书哈希用于验证在初始安装过程中从移动网络操作员的网页或捕获门户发送的预配文件的数字签名。 这支持在安装移动宽带应用之前用户购买服务的方案。 应将这两个字段的格式设置为可分辨名称，并且必须与用于对购买网站上的预配文件进行签名的数字证书的 " **使用者** " 和 " **颁发者** " 字段相匹配。 有关可分辨名称的详细信息，请参阅 [Internet 工程任务组网站上的可分辨名称的字符串表示形式](https://www.ietf.org/rfc/rfc4514.txt)中的 RFC 4514 部分。

    有关预配的详细信息，请参阅 [服务元数据包架构参考](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/service-metadata-package-schema-reference)。

 

