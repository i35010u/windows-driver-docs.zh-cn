---
title: WISPr 身份验证概述
description: WISPr 身份验证概述
ms.assetid: 49782d7f-c2f9-408d-971c-1af4d93d4d8d
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: c88a20513570bbe0b87407bd43961785ca70fc45
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608546"
---
# <a name="wispr-authentication-overview"></a>WISPr 身份验证概述


漫游 (WISPr) 无线 Internet 服务提供商的支持热点包括在其类似于以下的强制网络门户页面中的有效负载：

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

智能客户端，如 Windows，解释此 XML （它包含在 HTML 注释以避免其显示给客户），若要了解必须在其中提交用户的凭据。

当客户手动连接到支持 WISPr 的网络时，他们将看到以下提示：

![wispr 提示符](images/fig1-mb-wispr-auth-prompt.jpg)

选择的客户**否，我需要注册**定向到强制网络门户。 选择的客户**是的我将在其中输入我的用户名和密码**系统会提示输入其凭据。 这些凭据提供给你的网站，并在用户成功进行身份验证后连接。

移动宽带应用可以自动提供凭据，或通过使用定制的购买或身份验证流来替换提示输入凭据。 这需要网络支持 WISPr，并在用户连接到网络之前安装该应用。

如果你的网络提供 WISPr 向客户端通过使用某些用户代理字符串，用户将看不到此提示，并不能手动输入凭据。 但是，您的应用程序仍然可以参与 WISPr 身份验证通过时创建的网络配置文件包含相应的 UserAgent。

本节包括下列主题：

-   [热点身份验证的预配](provisioning-for-hotspot-authentication.md)

-   [处理大量的 Ssid](handling-large-numbers-of-ssids.md)

-   [处理热点身份验证事件](handling-the-hotspot-authentication-event.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[热点身份验证方法](hotspot-authentication-methods.md)

 

 






