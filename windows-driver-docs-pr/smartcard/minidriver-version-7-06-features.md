---
title: 微型驱动程序版本 7.06 功能
description: 微型驱动程序版本 7.06 功能
ms.assetid: 6066C6F9-DF03-4886-A5AE-FFE50B2B34D8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa4c0c1a624b414ee29be276326a8a5127b17218
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356688"
---
# <a name="minidriver-version-706-features"></a>微型驱动程序版本 7.06 功能


在此版本中引入以下功能。

## <a name="span-idsecurekeyinjectionspanspan-idsecurekeyinjectionspanspan-idsecurekeyinjectionspansecure-key-injection"></a><span id="Secure_Key_Injection"></span><span id="secure_key_injection"></span><span id="SECURE_KEY_INJECTION"></span>安全密钥注入


此功能非常有用，如果应用程序，在从智能卡断开连接的计算机运行，必须将敏感数据导入到其他计算机连接智能卡。

安全密钥注入的一个典型情况是当证书颁发机构 (CA) 的服务器上运行的是，必须执行以下操作：

-   生成服务器上的密钥对。
-   将用户密钥存档。
-   导入到智能卡插入到用户的计算机中的密钥对。

开发人员可以使用引入的安全密钥注入以提供以下新 Api 和数据结构：

-   允许智能卡框架，以确定卡片是否支持安全密钥注入的属性的支持。
-   建立如 Pin、 管理员密钥和非对称密钥对数据进行加密的对称密钥。 会话密钥然后导入到智能卡。
-   加密并将数据封装到可导入到和智能卡上处理的格式。
-   使用智能卡上的会话密钥解密已加密的数据。

此版本的规范中定义了以下用于传递加密的数据结构：

-   [**卡\_进行身份验证**](https://docs.microsoft.com/previous-versions/dn468744(v=vs.85))
-   [**卡片\_进行身份验证\_响应**](https://docs.microsoft.com/previous-versions/dn468745(v=vs.85))
-   [**卡片\_更改\_身份验证器**](https://docs.microsoft.com/previous-versions/dn468746(v=vs.85))
-   [**卡片\_更改\_身份验证器\_响应**](https://docs.microsoft.com/previous-versions/dn468747(v=vs.85))
-   [**卡片\_加密\_数据**](https://docs.microsoft.com/previous-versions/dn468749(v=vs.85))
-   [**CARD\_IMPORT\_KEYPAIR**](https://docs.microsoft.com/previous-versions/dn468750(v=vs.85))

此规范的版本 7 中定义的安全密钥注入以下卡属性。 有关这些属性的详细信息，请参阅[ **CardGetProperty**](https://docs.microsoft.com/previous-versions/dn468729(v=vs.85))。

-   CP\_键\_导入\_支持
-   CP\_枚举\_算法
-   CP\_填充\_方案
-   CP\_链接\_模式

此规范的版本 7 中的安全密钥注入中添加了以下 Api。 有关详细信息，请参阅[安全密钥注入](secure-key-injection.md)。

服务器功能：

-   [**MDEncryptData**](https://docs.microsoft.com/previous-versions/dn468756(v=vs.85))
-   [**MDImportSessionKey**](https://docs.microsoft.com/previous-versions/dn468757(v=vs.85))

共享的函数：

-   [**CardDestroyKey**](https://docs.microsoft.com/previous-versions/dn468720(v=vs.85))
-   [**CardGetAlgorithmProperty**](https://docs.microsoft.com/previous-versions/dn468722(v=vs.85))
-   [**CardGetKeyProperty**](https://docs.microsoft.com/previous-versions/dn468728(v=vs.85))
-   [**CardGetSharedKeyHandle**](https://docs.microsoft.com/previous-versions/dn468730(v=vs.85))
-   [**CardProcessEncryptedData**](https://docs.microsoft.com/previous-versions/dn468732(v=vs.85))
-   [**CardSetKeyProperty**](https://docs.microsoft.com/previous-versions/dn468739(v=vs.85))

客户端功能：

-   [**CardImportSessionKey**](https://docs.microsoft.com/previous-versions/dn468731(v=vs.85))

## <a name="span-idsupportforrsapaddingremovaloperationsinthesmartcardspanspan-idsupportforrsapaddingremovaloperationsinthesmartcardspanspan-idsupportforrsapaddingremovaloperationsinthesmartcardspansupport-for-rsa-padding-removal-operations-in-the-smart-card"></a><span id="Support_for_RSA_Padding_Removal_Operations_in_the_Smart_Card"></span><span id="support_for_rsa_padding_removal_operations_in_the_smart_card"></span><span id="SUPPORT_FOR_RSA_PADDING_REMOVAL_OPERATIONS_IN_THE_SMART_CARD"></span>对 RSA 填充在智能卡中的删除操作的支持


智能卡微型驱动程序接口的版本 7 允许智能卡供应商为 RSA 填充在智能卡本身中的删除操作提供支持。 基本 CSP/KSP 删除填充时，这可以防止遭受密码文本攻击。 此增强功能还会删除原始 RSA 解密操作由微型驱动程序的要求。

第 7 版还提供对较旧卡不支持内部的 （或 OnCard） 填充删除的支持。 这样，这些数据卡以继续使用基本 CSP/KSP 提供的填充删除功能。

有关详细信息，请参阅[ **PFN\_CSP\_UNPAD\_数据**](https://docs.microsoft.com/previous-versions/dn468771(v=vs.85))并[ **CardRSADecrypt** ](https://docs.microsoft.com/previous-versions/dn468737(v=vs.85))此规范中更高版本。

## <a name="span-idsmartcardplugandplayspanspan-idsmartcardplugandplayspanspan-idsmartcardplugandplayspansmart-card-plug-and-play"></a><span id="Smart_Card_Plug_and_Play"></span><span id="smart_card_plug_and_play"></span><span id="SMART_CARD_PLUG_AND_PLAY"></span>智能卡即插


徽标认证智能卡首先插入到的卡读卡器连接到 Windows 7 计算机，插 framework 搜索兼容的微型驱动程序在 Windows 更新中发布的。 如果找到微型驱动程序，插将自动从 Windows 更新下载微型驱动程序，并将其安装在计算机。

有关详细信息，请参阅[智能卡即插](smart-card-plug-and-play.md)。

## <a name="span-idcardcreatecontainerexspanspan-idcardcreatecontainerexspanspan-idcardcreatecontainerexspan-cardcreatecontainerex"></a><span id="_CardCreateContainerEx"></span><span id="_cardcreatecontainerex"></span><span id="_CARDCREATECONTAINEREX"></span> CardCreateContainerEx


此新 API 是扩展的功能[ **CardCreateContainer** ](https://docs.microsoft.com/previous-versions/dn468708(v=vs.85)) API。 除了创建的密钥容器，此函数将创建容器时建立的 PIN 关联。

有关详细信息，请参阅[ **CardCreateContainerEx** ](https://docs.microsoft.com/previous-versions/dn468709(v=vs.85))此规范中更高版本。

## <a name="span-idnewcardcontainerpropertyforecdsaecdhkeyassociationspanspan-idnewcardcontainerpropertyforecdsaecdhkeyassociationspanspan-idnewcardcontainerpropertyforecdsaecdhkeyassociationspannew-card-container-property-for-ecdsaecdh-key-association"></a><span id="New_Card_Container_Property_for_ECDSA_ECDH_Key_Association"></span><span id="new_card_container_property_for_ecdsa_ecdh_key_association"></span><span id="NEW_CARD_CONTAINER_PROPERTY_FOR_ECDSA_ECDH_KEY_ASSOCIATION"></span>ECDSA/ECDH 密钥关联的新卡容器属性


此新的容器属性将使用椭圆曲线 Diffie-hellman (ECDH) 密钥相关联的椭圆曲线数字签名算法 (ECDSA) 密钥。 每个 ECDSA 密钥与用于数据加密和解密的 ECDH 密钥配对。 此关联支持要求加密时使用 ECDSA 密钥的方案。

当登录证书的 ECDSA 证书时，通过使用相关联的 ECDH 密钥加密缓存的登录凭据。 在缓存的登录操作期间使用与用于用户登录的 ECDSA 密钥相关联的 ECDH 密钥解密从域控制器的数据。 在此情况下，智能卡可用于登录操作时在计算机处于脱机状态或无法访问域控制器。

有关详细信息，请参阅说明 CCP\_关联\_ECDH\_"卡和容器属性"中此规范更高版本中的键属性。

## <a name="span-idgenericinboxminidriverthatsupportspivspanspan-idgenericinboxminidriverthatsupportspivspanspan-idgenericinboxminidriverthatsupportspivspangeneric-inbox-minidriver-that-supports-piv"></a><span id="Generic_Inbox_Minidriver_that_Supports_PIV"></span><span id="generic_inbox_minidriver_that_supports_piv"></span><span id="GENERIC_INBOX_MINIDRIVER_THAT_SUPPORTS_PIV"></span>泛型收件箱微型驱动程序支持 PIV


操作系统从 Windows 7 开始，包括收件箱泛型微型驱动程序，可使用智能卡支持的个人标识验证 (PIV) 卡边缘和数据模型。

有关 piv 标准的详细信息，请参阅"有关个人标识验证 (PIV) 的联邦员工和合同工"网页。

有关 Windows 遵循来识别并对收件箱驱动程序的 PIV 网卡过程的详细信息，请参阅[Windows 收件箱智能卡微型驱动程序](windows-inbox-smart-card-minidriver.md)。

 

 





