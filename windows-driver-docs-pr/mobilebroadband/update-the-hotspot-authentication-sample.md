---
title: 更新热点身份验证示例
description: 更新热点身份验证示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecf1162b36009a3413700056cd03568bd150d52e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815041"
---
# <a name="update-the-hotspot-authentication-sample"></a>更新热点身份验证示例


[热点身份验证示例](/samples/browse/)项目使用默认的运营商 ID 和应用程序家族名称。 若要在自己的测试环境中使用此示例，必须更改以下项：

-   **更新你的运营商 ID** 如果要发布移动宽带应用，这应该是与应用和服务元数据关联的体验 ID。 如果你是仅 Wi-fi 操作员，则生成新的 GUID 作为你的公司 ID。

-   **更新 SSID** 用于测试的 SSID 应匹配预配文件中的 SSID，并且必须提供捕获的门户和 WISPr 质询来连接客户端。

-   **签署预配文件** 如果你是仅 Wi-fi 操作员，则必须对预配文件进行签名。 在 Windows 8 SDK 或 Windows 8.1 SDK 中，查找 **ProvisioningTestHelper.psd1** 的工具。 将此导入到 PowerShell 会话中，以添加以下四个附加 cmdlet：

    -   **安装-TestEVCert** 生成新的 CA 证书，在测试计算机上将其注册为受信任的 EV SSL 提供程序，并使用它来生成 EV 证书并对其进行签名，以便在签名时使用。

    -   **Convertto-html-SignedXml** 使用 (为测试生成的 EV 证书，或由第三方提供程序颁发的 EV 证书) 将 XML-DSig 签名应用到预配元数据 XML 文件。 受信任的证书中的此签名会导致 Windows 将预配文件从没有关联硬件的移动宽带应用接受为有效。

    -   **SignedXml** 检查预配文件，以确保架构一致性和有效签名。

    -   **安装-RootCertFromFile** 在另一台电脑上应用测试根证书，以测试开发计算机以外的其他计算机上的客户端体验。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[热点身份验证应用入门](review-the-hotspot-authentication-sample.md)

 

