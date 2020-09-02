---
title: 微型驱动程序版本 7.06 功能
description: 微型驱动程序版本 7.06 功能
ms.assetid: 6066C6F9-DF03-4886-A5AE-FFE50B2B34D8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 723a1324cd9993f41159b52309fdf5ab85779b21
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381373"
---
# <a name="minidriver-version-706-features"></a>微型驱动程序版本 7.06 功能


此版本中引入了以下功能。

## <a name="span-idsecure_key_injectionspanspan-idsecure_key_injectionspanspan-idsecure_key_injectionspansecure-key-injection"></a><span id="Secure_Key_Injection"></span><span id="secure_key_injection"></span><span id="SECURE_KEY_INJECTION"></span>安全密钥注入


如果在与智能卡断开连接的计算机上运行的应用程序必须将敏感数据导入到连接到其他计算机的智能卡，则此功能非常有用。

安全密钥注入的一个典型方案是在服务器上运行的证书颁发机构 (CA) ，必须执行以下操作：

-   在服务器上生成密钥对。
-   将用户密钥存档。
-   将密钥对导入到用户计算机中插入的智能卡。

开发人员可以使用为安全密钥注入引入的新 Api 和数据结构来提供以下内容：

-   支持允许智能卡框架确定卡是否支持安全密钥注入的属性。
-   建立对称密钥来加密数据，如 Pin、管理员密钥和非对称密钥对。 然后，可以将会话密钥导入到智能卡。
-   将数据加密并封装到智能卡上可以导入和处理的格式。
-   用智能卡上的会话密钥对加密的数据进行解密。

在此版本的规范中定义了以下用于传递加密数据的结构：

-   [**智能卡 \_ 身份验证**](/previous-versions/dn468744(v=vs.85))
-   [**智能卡 \_ 身份验证 \_ 响应**](/previous-versions/dn468745(v=vs.85))
-   [**卡 \_ 更改 \_ 身份验证器**](/previous-versions/dn468746(v=vs.85))
-   [**卡 \_ 更改 \_ 验证器 \_ 响应**](/previous-versions/dn468747(v=vs.85))
-   [**卡 \_ 加密 \_ 数据**](/previous-versions/dn468749(v=vs.85))
-   [**卡 \_ 导入 \_ 密钥**](/previous-versions/dn468750(v=vs.85))

此规范的版本7中定义了安全密钥注入的以下卡属性。 有关这些属性的详细信息，请参阅 [**CardGetProperty**](/previous-versions/dn468729(v=vs.85))。

-   CP \_ 密钥 \_ 导入 \_ 支持
-   CP \_ 枚举 \_ 算法
-   CP \_ 填充 \_ 方案
-   CP \_ 链接 \_ 模式

为此规范的版本7中的安全密钥注入添加了以下 Api。 有关详细信息，请参阅 [安全密钥注入](secure-key-injection.md)。

服务器函数：

-   [**MDEncryptData**](/previous-versions/dn468756(v=vs.85))
-   [**MDImportSessionKey**](/previous-versions/dn468757(v=vs.85))

共享函数：

-   [**CardDestroyKey**](/previous-versions/dn468720(v=vs.85))
-   [**CardGetAlgorithmProperty**](/previous-versions/dn468722(v=vs.85))
-   [**CardGetKeyProperty**](/previous-versions/dn468728(v=vs.85))
-   [**CardGetSharedKeyHandle**](/previous-versions/dn468730(v=vs.85))
-   [**CardProcessEncryptedData**](/previous-versions/dn468732(v=vs.85))
-   [**CardSetKeyProperty**](/previous-versions/dn468739(v=vs.85))

客户端函数：

-   [**CardImportSessionKey**](/previous-versions/dn468731(v=vs.85))

## <a name="span-idsupport_for_rsa_padding_removal_operations_in_the_smart_cardspanspan-idsupport_for_rsa_padding_removal_operations_in_the_smart_cardspanspan-idsupport_for_rsa_padding_removal_operations_in_the_smart_cardspansupport-for-rsa-padding-removal-operations-in-the-smart-card"></a><span id="Support_for_RSA_Padding_Removal_Operations_in_the_Smart_Card"></span><span id="support_for_rsa_padding_removal_operations_in_the_smart_card"></span><span id="SUPPORT_FOR_RSA_PADDING_REMOVAL_OPERATIONS_IN_THE_SMART_CARD"></span>支持智能卡中的 RSA 填充删除操作


智能卡微型驱动程序接口的版本7允许智能卡供应商为智能卡本身中的 RSA 填充删除操作提供支持。 当基本 CSP/KSP 删除填充时，这会阻止泄露密码攻击。 此增强功能还消除了微型驱动程序对原始 RSA 解密操作的要求。

版本7还为不支持内部 (或 OnCard) 填充删除的旧卡提供支持。 这允许这些卡继续使用基本 CSP/KSP 提供的填充删除功能。

有关详细信息，请参阅此规范中的 [**PFN \_ CSP \_ UNPAD \_ DATA**](/previous-versions/dn468771(v=vs.85)) 和 [**CardRSADecrypt**](/previous-versions/dn468737(v=vs.85)) 。

## <a name="span-idsmart_card_plug_and_playspanspan-idsmart_card_plug_and_playspanspan-idsmart_card_plug_and_playspansmart-card-plug-and-play"></a><span id="Smart_Card_Plug_and_Play"></span><span id="smart_card_plug_and_play"></span><span id="SMART_CARD_PLUG_AND_PLAY"></span>智能卡即插即用


首次将徽标认证智能卡插入到连接到 Windows 7 计算机的卡读卡器中时，即插即用框架会搜索 Windows 更新中发布的兼容微型驱动程序。 如果找到微型驱动程序，则即插即用会自动从 Windows 更新下载微型驱动程序，并将其安装在计算机中。

有关详细信息，请参阅 [智能卡即插即用](smart-card-plug-and-play.md)。

## <a name="span-id_cardcreatecontainerexspanspan-id_cardcreatecontainerexspanspan-id_cardcreatecontainerexspan-cardcreatecontainerex"></a><span id="_CardCreateContainerEx"></span><span id="_cardcreatecontainerex"></span><span id="_CARDCREATECONTAINEREX"></span> CardCreateContainerEx


这个新的 API 扩展了 [**CardCreateContainer**](/previous-versions/dn468708(v=vs.85)) API 的功能。 除了创建密钥容器外，此函数还会在创建容器时建立 PIN 关联。

有关详细信息，请参阅本规范后面的 [**CardCreateContainerEx**](/previous-versions/dn468709(v=vs.85)) 。

## <a name="span-idnew_card_container_property_for_ecdsa_ecdh_key_associationspanspan-idnew_card_container_property_for_ecdsa_ecdh_key_associationspanspan-idnew_card_container_property_for_ecdsa_ecdh_key_associationspannew-card-container-property-for-ecdsaecdh-key-association"></a><span id="New_Card_Container_Property_for_ECDSA_ECDH_Key_Association"></span><span id="new_card_container_property_for_ecdsa_ecdh_key_association"></span><span id="NEW_CARD_CONTAINER_PROPERTY_FOR_ECDSA_ECDH_KEY_ASSOCIATION"></span>用于 ECDSA/ECDH 密钥关联的新卡容器属性


这个新的容器属性将椭圆曲线数字签名算法 (ECDSA) 键与椭圆曲线 Diffie-hellman (ECDH) 密钥相关联。 每个 ECDSA 密钥与用于数据加密和解密的 ECDH 密钥成对出现。 使用 ECDSA 密钥时，此关联支持要求加密的方案。

如果登录证书是 ECDSA 证书，则使用关联的 ECDH 密钥对缓存的登录凭据进行加密。 在缓存的登录操作期间，将使用与用于用户登录的 ECDSA 密钥关联的 ECDH 密钥来解密域控制器中的数据。 在这种情况下，当计算机脱机或无法访问域控制器时，可以使用智能卡登录操作。

有关详细信息，请参阅 \_ \_ \_ 此规范后面的 "卡和容器属性" 中与 CCP 关联的 ECDH 密钥属性的描述。

## <a name="span-idgeneric_inbox_minidriver_that_supports_pivspanspan-idgeneric_inbox_minidriver_that_supports_pivspanspan-idgeneric_inbox_minidriver_that_supports_pivspangeneric-inbox-minidriver-that-supports-piv"></a><span id="Generic_Inbox_Minidriver_that_Supports_PIV"></span><span id="generic_inbox_minidriver_that_supports_piv"></span><span id="GENERIC_INBOX_MINIDRIVER_THAT_SUPPORTS_PIV"></span>支持 PIV 的通用收件箱微型驱动程序


从 Windows 7 开始，操作系统包含一个收件箱通用微型驱动程序，它可用于支持个人身份验证的智能卡 (PIV) 卡边缘和数据模型。

有关 PIV 的详细信息，请参阅 "关于个人身份验证 (PIV) 联邦员工和合同工" 网页。

有关 Windows 用于标识 PIV 卡并将其与收件箱驱动程序配对的过程的详细信息，请参阅 [Windows 收件箱智能卡微型驱动程序](windows-inbox-smart-card-minidriver.md)。

 

