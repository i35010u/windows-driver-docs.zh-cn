---
title: 更新热点身份验证示例
description: 更新热点身份验证示例
ms.assetid: 68ebcdee-7b21-4177-b032-ba725ad2aee4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9e74240085dcd4e327499732cdd3a0f129f5bc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569493"
---
# <a name="update-the-hotspot-authentication-sample"></a>更新热点身份验证示例


[热点身份验证示例](https://go.microsoft.com/fwlink/p/?linkid=313215)项目使用默认载波 ID 和应用程序系列名称。 若要在测试环境中使用该示例，必须更改以下项：

-   **更新你的承运人 ID**如果发布的移动宽带应用，这应是与你的应用程序和服务元数据相关联的体验 ID。 如果您是仅限 Wi Fi 操作员，，生成新的 GUID 用作公司的 id。

-   **更新 SSID**用于测试的 SSID 应与配置文件中的 SSID 和必须产品/服务强制网络门户网站和 WISPr 质询到连接的客户端。

-   **预配文件进行签名**如果您是仅限 Wi Fi 操作员，您必须预配文件进行签名。 在 Windows 8 SDK 或 Windows 8.1 SDK 中，找到工具**ProvisioningTestHelper.psd1**。 将此导入 PowerShell 会话，并添加以下四个其他 cmdlet:

    -   **安装 TestEVCert**生成新的 CA 证书、 将其注册到测试计算机作为受信任的 EV SSL 提供程序，并使用它来生成并在签名中使用的 EV 证书进行签名。

    -   **ConvertTo SignedXml**使用 EV 证书 （对于测试，生成或由第三方提供商发行） 将 XML DSig 签名应用于预配元数据 XML 文件。 此签名从受信任的证书将导致 Windows 接受为有效从具有任何关联的硬件的移动宽带应用预配的文件。

    -   **测试 SignedXml**检查预配文件以确保架构一致性和有效的签名。

    -   **安装 RootCertFromFile**适用不同的 PC，以测试客户端体验开发 PC 的机器上测试根证书。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[热点身份验证应用入门](get-started-with-a-hotspot-authentication-app.md)

 

 






