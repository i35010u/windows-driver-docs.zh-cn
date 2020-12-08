---
title: WISPr 身份验证概述
description: WISPr 身份验证概述
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: 72d579481485319c8edcfbbd7d78daa1f2a5870a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820621"
---
# <a name="wispr-authentication-overview"></a>WISPr 身份验证概述

无线 Internet 服务提供商漫游 (支持 WISPr) 的热点在其固定门户页面中包含有效负载，类似于以下内容：

``` syntax
<HTML>
<!--
    <?xml version=”1.0” encoding=”UTF-8”?>
    <WISPAccessGatewayParam xmlns:xsi=”http://www.w3.org/2001/XMLSchema-instance”
      xsi:noNamespaceSchemaLocation=”http://www.acmewisp.com/WISPAccessGatewayParam.xsd”>
      <Redirect>
        <AccessProcedure>1.0</AccessProcedure>
        <AccessLocation>Hotel Contoso Guest Network</AccessLocation>
        <LocationName>Hotel Contoso</LocationName>
        <LoginURL>https://captiveportal.com/login</LoginURL>
        <MessageType>100</MessageType>
        <ResponseCode>0</ResponseCode>
      </Redirect>
    </WISPAccessGatewayParam>
-->
</HTML>
```

智能客户端（如 Windows）会解释 HTML 注释中包含的此 XML (，以避免向客户) 显示用户的凭据。

当客户手动连接到支持 WISPr 的网络时，会看到以下提示：

![wispr 提示符](images/fig1-mb-wispr-auth-prompt.jpg)

如果客户选择 **"否"，则需要** 将其注册到你的捕获门户。 如果客户选择 **"是"，则输入用户名和密码** 时，会提示用户输入其凭据。 这些凭据将提供给你的网站，并在成功身份验证后连接用户。

移动宽带应用可以使用定制的购买或身份验证流自动提供凭据或替换凭据提示。 这要求网络支持 WISPr，并要求在用户连接到网络之前安装该应用。

如果你的网络使用特定的 UserAgent 字符串向客户端提供 WISPr，用户将看不到此提示，无法手动输入凭据。 但是，在创建网络配置文件时，你的应用程序仍然可以通过包含相应的 UserAgent 来参与 WISPr 身份验证。

本节包括下列主题：

- [针对热点身份验证的预配](provisioning-for-hotspot-authentication.md)

- [处理大量的 SSID](handling-large-numbers-of-ssids.md)

- [处理热点身份验证事件](handling-the-hotspot-authentication-event.md)
