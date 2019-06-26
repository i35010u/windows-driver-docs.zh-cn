---
title: 开发人员指南
description: 本主题讨论用于处理和开发智能卡微型驱动程序的一般准则。
ms.assetid: 48999DF6-3AC2-4DEA-8ABC-C427237B31E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cef25db934557a47597f9a103b40c8c7913636d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393102"
---
# <a name="developer-guidelines"></a>开发人员指南


本主题讨论的开发人员使用，和/或开发智能卡微型驱动程序-，告知你的智能卡和其关联的应用程序的预期的行为的一般指导原则。

## <a name="span-idgeneraldesignguidelinesspanspan-idgeneraldesignguidelinesspanspan-idgeneraldesignguidelinesspangeneral-design-guidelines"></a><span id="General_Design_Guidelines"></span><span id="general_design_guidelines"></span><span id="GENERAL_DESIGN_GUIDELINES"></span>一般设计准则


有关如何分发卡微型驱动程序，如何映射逻辑卡文件系统和其他微型驱动程序设计指南，请参阅**一般设计准则**部分下[智能卡微型驱动程序概述](smart-card-minidriver-overview.md)。

## <a name="span-idchallengeresponsemethodofunblockingsmartcardpinspanspan-idchallengeresponsemethodofunblockingsmartcardpinspanspan-idchallengeresponsemethodofunblockingsmartcardpinspanchallengeresponse-method-of-unblocking-smart-card-pin"></a><span id="Challenge_Response_Method_of_Unblocking_Smart_Card_PIN"></span><span id="challenge_response_method_of_unblocking_smart_card_pin"></span><span id="CHALLENGE_RESPONSE_METHOD_OF_UNBLOCKING_SMART_CARD_PIN"></span>解除锁定智能卡 PIN 的质询/响应方法


若要成功使用此机制来取消阻止用户卡管理员，管理员必须能够标识，并使用，以便它们可以正确生成已颁发的质询的响应数据存储在卡的管理员密钥。

若要执行此操作的一种方法是使用卡标识符来唯一标识卡。 （卡标识符。 卡片的唯一标识符）这可以以某种形式表示，向用户在 UI 中，但否则可以编写一个程序将适当的 APDU 命令发送到要读取此信息的卡片。

此信息可以然后允许管理员以确定在卡上的机密密钥，并计算正确响应已颁发给用户的质询数据。

假定存储在卡上的管理员密钥由使用只有有效且受信任的管理员 （最好是尽可能少） 才能访问某些安全机制。 但是，这超出了本规范的范畴。

有关详细信息，请参阅以下"质询/响应机制"部分。

## <a name="span-idenhancedpinsupportspanspan-idenhancedpinsupportspanspan-idenhancedpinsupportspanenhanced-pin-support"></a><span id="Enhanced_PIN_Support"></span><span id="enhanced_pin_support"></span><span id="ENHANCED_PIN_SUPPORT"></span>增强的 PIN 支持


版本 6.0 支持多个 PIN 支持灵活的体系结构。 此体系结构引入了新的每个角色对应于一个 PIN 标识符的角色概念。 PIN 标识符用于从卡中，提取 PIN 信息，以及若要将 PIN 与密钥容器相关联。

标识符包含一个数字，当前限制为 0 through7。 我们还引入了这一概念 PIN\_设置，这是一个位掩码，可以从 PIN 标识符生成。 当前仅低 8 位用于 PIN 设置。 我们还可以选择使用剩余的位来指示条件如 and、 或，或其他信息，我们可能会发现其在将来很有用。 我们选择了这种方法，以便轻松要强制实施的卡片的位掩码。

假定，用户进行身份验证使用角色 3，对应于 PIN \#3。 这会转换为位掩码 0000 0100 (基数为 2)。 卡可以将它保存为当前经过身份验证的 ID，并通过执行按位 AND 运算时可以轻松验证密钥和 Pin 的访问控制规则。 设计允许同时在卡上使用多个经过身份验证的身份，这是必需的支持 v6 卡微型驱动程序的卡。 例如，如果 PIN \#1 进行身份验证，并随后固定\#2 进行身份验证，应允许任何这些引脚控制的操作。

## <a name="span-idsessionpinsandsecurepinchannelspanspan-idsessionpinsandsecurepinchannelspanspan-idsessionpinsandsecurepinchannelspan-session-pins-and-secure-pin-channel"></a><span id="_Session_PINs_and_Secure_PIN_Channel"></span><span id="_session_pins_and_secure_pin_channel"></span><span id="_SESSION_PINS_AND_SECURE_PIN_CHANNEL"></span> 会话 Pin 和安全 PIN 通道


当 Windows 必须建立用于 PIN 身份验证的安全 PIN 通道时，微型驱动程序被执行以下一系列操作。 为遵从美国，微型驱动程序与卡必须按以下顺序与兼容。 具体而言，会话 Pin 应进程之间转让和最后一个特定长度的时间。 (我们建议，任何会话 PIN 是有效的卡的冷重置之前使用的卡\_进行身份验证\_会话\_PIN 标志，即使[ **CardAuthenticateEx** ](https://docs.microsoft.com/previous-versions/dn468703(v=vs.85))被调用，将生成\_会话\_PIN 标志设置。)

应支持以下行为：

1.  应用程序 A，受信任的系统进程，获取智能卡的句柄，并收集 PIN。
2.  应用程序随后将调用卡片[ **CardAuthenticateEx** ](https://docs.microsoft.com/previous-versions/dn468703(v=vs.85))微型驱动程序函数并传递 PIN 收集并设置卡\_进行身份验证\_生成\_会话\_PIN 标志。 这不会导致要将其解锁的卡片。
3.  应用程序 A 存储会话 PIN 的已生成并释放句柄的卡和卡微型驱动程序。 此卡不冷重置。
4.  应用程序 A 发送了会话 PIN 和读取器具有到应用程序 B 的步骤 1 中获取的卡的名称
5.  应用程序 B 将获取在同一张卡，如 1 中所示。
6.  应用程序 B 调用[ **CardAuthenticateEx** ](https://docs.microsoft.com/previous-versions/dn468703(v=vs.85)) PIN 在会话中传递，并设置卡\_进行身份验证\_会话\_PIN 标志。 如果会话 PIN 是否仍然有效，卡应经过身份验证和有效使用。
7.  完成应用程序 B 使用卡，它会调用[ **CardDeauthenticateEx** ](https://docs.microsoft.com/previous-versions/dn468713(v=vs.85))以 deauthorize 卡。

此行为具有以下实际限制：

-   卡必须来声明其可以通过为 CP 返回适当的值来处理会话 Pin\_卡\_PIN\_强度\_验证。
-   依赖于具有每个验证的 PIN 卡都不符合此系统。
-   可以有多个应用程序，它们确定在任何时候是有效的会话 Pin。 如果只有一个会话 PIN 是可能对于每个插针，建议的以下实现：

    -   卡应记住的最新的会话已生成的 PIN。
    -   如果显示了无效会话 PIN，卡应成功通过身份验证，和如果支持，为会话 PIN 递减重试计数器。 如果重试计数达到 0 下, 一次身份验证尝试无效，该会话 PIN 应失效。
    -   随后的会话 PIN 演示文稿应失败，直至新的会话 PIN 进行协商。
-   会话 PIN 必须能够从不同的应用程序在系统上使用。
-   会话 PIN 必须不只是固定的编码。
-   此系统的安全性被限制为会话 PIN 强度和用于生成它的协商协议。 实际会话 PIN 协商已超出本规范的范畴。 只不过它按本节中所述方式工作，我们会在设计上进行没有要求。
-   会话 PIN 仍被视为有价值，并应被视为机密。
-   卡应能够检测到无效的会话 PIN。

## <a name="span-idread-onlycardsspanspan-idread-onlycardsspanspan-idread-onlycardsspanread-only-cards"></a><span id="Read-Only_Cards"></span><span id="read-only_cards"></span><span id="READ-ONLY_CARDS"></span>只读的卡


地址之外的基本 CSP/KSP 环境和是本质上是只读的我们引入了新的只读卡概念个性化的卡。 如果卡是只读的它必须播发通过这[ **CardGetProperty** ](https://docs.microsoft.com/previous-versions/dn468729(v=vs.85))函数 （请参阅本节前面在本规范中）。

只读卡必须支持版本 7 卡微型驱动程序接口的一个子集，并且不需要支持管理员 PIN。

下表列出了只读的卡必须支持的函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数名称</th>
<th align="left">必需</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468701(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAcquireContext&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468701(v=vs.85))"><strong>CardAcquireContext</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468715(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteContext&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468715(v=vs.85))"><strong>CardDeleteContext</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468704(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAuthenticatePin&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468704(v=vs.85))"><strong>CardAuthenticatePin</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468723(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetChallenge&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468723(v=vs.85))"><strong>CardGetChallenge</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468702(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAuthenticateChallenge&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468702(v=vs.85))"><strong>CardAuthenticateChallenge</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468712(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeauthenticate&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468712(v=vs.85))"><strong>CardDeauthenticate</strong></a></td>
<td align="left">是 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468742(v=vs.85)" data-raw-source="[&lt;strong&gt;CardUnblockPin&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468742(v=vs.85))"><strong>CardUnblockPin</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468705(v=vs.85)" data-raw-source="[&lt;strong&gt;CardChangeAuthenticator&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468705(v=vs.85))"><strong>CardChangeAuthenticator</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468710(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateDirectory&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468710(v=vs.85))"><strong>CardCreateDirectory</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468716(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468716(v=vs.85))"><strong>CardDeleteDirectory</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468736(v=vs.85)" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468736(v=vs.85))"><strong>CardReadFile</strong></a></td>
<td align="left">是</td>
<td align="left">卡微型驱动程序必须模拟文件系统。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468711(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468711(v=vs.85))"><strong>CardCreateFile</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468727(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetFileInfo&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468727(v=vs.85))"><strong>CardGetFileInfo</strong></a></td>
<td align="left">是</td>
<td align="left">卡微型驱动程序必须模拟文件系统。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468743(v=vs.85)" data-raw-source="[&lt;strong&gt;CardWriteFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468743(v=vs.85))"><strong>CardWriteFile</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468711(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468711(v=vs.85))"><strong>CardDeleteFile</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468721(v=vs.85)" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468721(v=vs.85))"><strong>CardEnumFiles</strong></a></td>
<td align="left">是</td>
<td align="left">卡微型驱动程序必须模拟文件系统。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468734(v=vs.85)" data-raw-source="[&lt;strong&gt;CardQueryFreeSpace&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468734(v=vs.85))"><strong>CardQueryFreeSpace</strong></a></td>
<td align="left">是</td>
<td align="left">卡微型驱动程序必须模拟文件系统。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468733(v=vs.85)" data-raw-source="[&lt;strong&gt;CardQueryCapabilities&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468733(v=vs.85))"><strong>CardQueryCapabilities</strong></a></td>
<td align="left">是</td>
<td align="left">卡微型驱动程序必须模拟文件系统。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468708(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateContainer&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468708(v=vs.85))"><strong>CardCreateContainer</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468709(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateContainerEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468709(v=vs.85))"><strong>CardCreateContainerEx</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468714(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteContainer&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468714(v=vs.85))"><strong>CardDeleteContainer</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468725(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetContainerInfo&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468725(v=vs.85))"><strong>CardGetContainerInfo</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468737(v=vs.85)" data-raw-source="[&lt;strong&gt;CardRSADecrypt&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468737(v=vs.85))"><strong>CardRSADecrypt</strong></a></td>
<td align="left">是 （可选）</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468707(v=vs.85)" data-raw-source="[&lt;strong&gt;CardConstructDHAgreement&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468707(v=vs.85))"><strong>CardConstructDHAgreement</strong></a></td>
<td align="left">是 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468718(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeriveKey&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468718(v=vs.85))"><strong>CardDeriveKey</strong></a></td>
<td align="left">是 （可选）</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468719(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDestroyDHAgreement&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468719(v=vs.85))"><strong>CardDestroyDHAgreement</strong></a></td>
<td align="left">是 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468741(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSignData&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468741(v=vs.85))"><strong>CardSignData</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468735(v=vs.85)" data-raw-source="[&lt;strong&gt;CardQueryKeySizes&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468735(v=vs.85))"><strong>CardQueryKeySizes</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468703(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAuthenticateEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468703(v=vs.85))"><strong>CardAuthenticateEx</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468706(v=vs.85)" data-raw-source="[&lt;strong&gt;CardChangeAuthenticatorEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468706(v=vs.85))"><strong>CardChangeAuthenticatorEx</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468713(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeauthenticateEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468713(v=vs.85))"><strong>CardDeauthenticateEx</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468724(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetChallengeEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468724(v=vs.85))"><strong>CardGetChallengeEx</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468726(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetContainerProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468726(v=vs.85))"><strong>CardGetContainerProperty</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468738(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSetContainerProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468738(v=vs.85))"><strong>CardSetContainerProperty</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468729(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468729(v=vs.85))"><strong>CardGetProperty</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468740(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSetProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468740(v=vs.85))"><strong>CardSetProperty</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468757(v=vs.85)" data-raw-source="[&lt;strong&gt;MDImportSessionKey&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468757(v=vs.85))"><strong>MDImportSessionKey</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468756(v=vs.85)" data-raw-source="[&lt;strong&gt;MDEncryptData&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468756(v=vs.85))"><strong>MDEncryptData</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468731(v=vs.85)" data-raw-source="[&lt;strong&gt;CardImportSessionKey&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468731(v=vs.85))"><strong>CardImportSessionKey</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468730(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetSharedKeyHandle&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468730(v=vs.85))"><strong>CardGetSharedKeyHandle</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468722(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetAlgorithmProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468722(v=vs.85))"><strong>CardGetAlgorithmProperty</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468728(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetKeyProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468728(v=vs.85))"><strong>CardGetKeyProperty</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468739(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSetKeyProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468739(v=vs.85))"><strong>CardSetKeyProperty</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468720(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDestroyKey&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468720(v=vs.85))"><strong>CardDestroyKey</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468732(v=vs.85)" data-raw-source="[&lt;strong&gt;CardProcessEncryptedData&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468732(v=vs.85))"><strong>CardProcessEncryptedData</strong></a></td>
<td align="left">否 （可选）</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">图例</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">是</td>
<td align="left">必须实现此函数。</td>
</tr>
<tr class="even">
<td align="left">否</td>
<td align="left">入口点必须存在，并且必须返回 SCARD_E_UNSUPPORTED_FEATURE。</td>
</tr>
<tr class="odd">
<td align="left">否 （可选）</td>
<td align="left">该操作不需要为只读的卡片中，支持，但如果卡支持该操作可能会实现。 如果不受支持，入口点必须返回 SCARD_E_UNSUPPORTED_FEATURE。</td>
</tr>
<tr class="even">
<td align="left">是 （可选）</td>
<td align="left">根据其定义在此规范中，而不考虑卡是只读的应实现此函数。</td>
</tr>
</tbody>
</table>

 

开发为只读的卡微型驱动程序时，应考虑以下要求：

-   所有需的基本 CSP/KSP 文件、 只读的卡上必须存在除 msroots 文件 （如 cardcf 和 cardid） 之外 （或必须通过微型驱动程序界面虚拟化）。
-   只读的卡必须包含至少一个密钥保护的主卡在卡上 (即，角色\_用户) 的 PIN。
-   允许只读卡不包含管理密钥。 如果这是这种情况，应该微型驱动程序将不支持[ **CardGetChallenge**](https://docs.microsoft.com/previous-versions/dn468723(v=vs.85))， [ **CardAuthenticateChallenge** ](https://docs.microsoft.com/previous-versions/dn468702(v=vs.85))，并[ **CardUnblockPin**](https://docs.microsoft.com/previous-versions/dn468742(v=vs.85))。
-   查询时，只读的卡应返回 0 字节可用和 0 可用容器。
-   仅 CP\_父\_窗口和 CP\_PIN\_上下文\_应允许字符串属性只读的卡上设置。
-   为只读的卡中，CP\_支持\_赢取\_X509\_注册属性应为 false。

## <a name="span-idcachemodesspanspan-idcachemodesspanspan-idcachemodesspancache-modes"></a><span id="Cache_Modes"></span><span id="cache_modes"></span><span id="CACHE_MODES"></span>缓存模式


基本 CSP/KSP 支持三种不同模式的具体取决于返回的缓存模式缓存[ **CardGetProperty** ](https://docs.microsoft.com/previous-versions/dn468729(v=vs.85))调用使用参数 CP\_卡\_缓存\_模式：

-   如果返回的标志 CP\_缓存\_模式\_GLOBAL\_缓存和卡报告 CP\_读取\_仅\_卡属性为 TRUE，基本 CSP/KSP 数据缓存是全局缓存。 如果卡是只读的基本 CSP/KSP 不会写入到 cardcf 文件。 如果卡可以写入到基本 CSP/KSP，它将与现在进行操作。
-   详细了解 CP\_卡\_缓存\_模式和 CP\_缓存\_模式\_全局\_缓存，请参阅[ **CardGetProperty**](https://docs.microsoft.com/previous-versions/dn468729(v=vs.85)).
-   返回的标志时 CP\_缓存\_模式\_会话\_仅，基本 CSP/KSP 进行操作，以便检测到已删除或重新插入卡时清除数据缓存。 换而言之，我们定义一个会话，以便将卡插入和删除之间的跨度。
-   缓存还为每个进程执行，不是全局设置。 此模式下专为只读的卡不会更改在用户的 PC 上，但在一些政府工作站或其他外部站点。 （对于读/写卡，才支持此模式，但我们建议这些卡全局缓存。）
-   如果卡是只读的并且没有机会卡将更改用户的 PC （通过表示基本 CSP/KSP 以外），该应用程序应使用任何更高版本中要避免这种情况在其中缓存可能包含 st 此规范所述的缓存模式ale 数据。
-   当该标志是 CP\_缓存\_模式\_否\_缓存中，基本 CSP/KSP 不实现任何数据缓存。 此模式下专为不支持写入 cardcf 文件，但卡状态可在其中更改卡微型驱动程序。 卡微型驱动程序决定它是否想要执行任何缓存其层中。

## <a name="span-idchallengeresponsemechanismspanspan-idchallengeresponsemechanismspanspan-idchallengeresponsemechanismspan-challengeresponse-mechanism"></a><span id="_Challenge_Response_Mechanism"></span><span id="_challenge_response_mechanism"></span><span id="_CHALLENGE_RESPONSE_MECHANISM"></span> 质询/响应机制


卡微型驱动程序接口支持的质询/响应身份验证机制。 卡必须生成一个或多个 8 字节块为单位的一个挑战。 验证实体计算方法是通过使用运行具有 168 位密钥在 CBC 模式下操作的三重 DES (3DES) 加密的质询响应 （和忽略奇偶校验位）。

卡验证响应，使用以下方法之一：

-   重复上以前颁发的质询的加密操作，并比较结果。
-   解密响应和比较的质询结果。

如果生成的值是相同的身份验证是成功的。

在卡和身份验证的实体必须使用相同的对称密钥。

下面的示例代码详细介绍如何验证实体无法计算响应。 此代码不包括任何关联的保证，只是用作示例和指导。

```ManagedCPlusPlus
#include <windows.h>
#include <wincrypt.h>
#include <winscard.h>
#include <stdlib.h>
#include <stdio.h>
#include <memory.h>


int __cdecl wmain(int argc, __in_ecount(argc) WCHAR **wargv)
{
    //Acquire the context Use CryptAcquireContext

    HCRYPTPROV hProv= 0;
    DWORD dwMode=CRYPT_MODE_ECB;
    BYTE *pbLocData = NULL,tempbyte;
    DWORD cbLocData = 8, count = 0;
    HCRYPTKEY hKey = 0;
    BYTE rgEncByte [] = {0xA8,0x92,0xD7,0x56,0x01,0x61,0x7C,0x5D };

    BYTE DesKeyBlob [] = {
        0x08, 0x02, 0x00, 0x00, 0x03, 0x66, 0x00, 0x00,
        0x18, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00
    };

    pbLocData = (BYTE *) malloc (sizeof(BYTE)*cbLocData);
    memcpy(pbLocData,rgEncByte,cbLocData);

    if (!CryptAcquireContext(
            &hProv,
            NULL,
            L"Microsoft Enhanced Cryptographic Provider V1.0",
            PROV_RSA_FULL,
            CRYPT_VERIFYCONTEXT))
    {
        printf("Acquire context failed with 0x%08x \n", GetLastError());
        goto Cleanup;
    }
    if (!CryptImportKey(
            hProv,
            DesKeyBlob,
            sizeof(DesKeyBlob),
            0,
            0,
            &hKey ) )
    {
        printf("Error 0x%08x in importing the 3Des key \n", GetLastError());
        goto Cleanup;
    }
    if (!CryptSetKeyParam(
            hKey,
            KP_MODE,
            (BYTE *)&dwMode,
            0))
    {
        printf("Error 0x%08x in CryptSetKeyParam \n", GetLastError());
        goto Cleanup;
    }
    if (!CryptEncrypt(
            hKey,
            0,
            FALSE,
            0,
            pbLocData,
            &cbLocData,
            cbLocData))
    {
        printf("Error 0x%08x in CryptEncrypt call \n", GetLastError());
        goto Cleanup;
    }

    for (count=0; count < cbLocData; ++count)
    {
        printf("0x%02x",pbLocData[count]);
    }
    printf("\n");

Cleanup:    
    if (hKey)
    {
        CryptDestroyKey(hKey);
        hKey = 0;
    }
    if (pbLocData)
    {
        free(pbLocData);
        pbLocData = NULL;
    }
    if (hProv)
    {
        CryptReleaseContext(hProv,0);
    }

    return 0;
}
```

## <a name="span-idinteroperabilitywithmsrootsspanspan-idinteroperabilitywithmsrootsspanspan-idinteroperabilitywithmsrootsspan-interoperability-with-msroots"></a><span id="_Interoperability_with_msroots"></span><span id="_interoperability_with_msroots"></span><span id="_INTEROPERABILITY_WITH_MSROOTS"></span> 与 msroots 互操作性


Msroots 文件是 PKCS \#7 格式的证书适用于应用商店企业信任的根。 （该文件是使用空内容和一个空的签名证书的包编写和读取的基本 CSP。）卡微型驱动程序开发人员不需要在卡微型驱动程序来处理此文件中编写任何特殊代码。 将证书存储中 msroots 文件时，属性，如代码\_因为 msroots 文件以不同于计算机存储区的格式存储证书签名 EKU 不会传播到智能卡。 想要读取或写入此文件从其他应用程序开发人员可以使用下面的示例代码段来访问数据。

### <a name="span-idreadoperationsspanspan-idreadoperationsspanspan-idreadoperationsspanread-operations"></a><span id="Read_operations"></span><span id="read_operations"></span><span id="READ_OPERATIONS"></span>读取操作

```ManagedCPlusPlus
if (FALSE == CryptQueryObject(CERT_QUERY_OBJECT_BLOB,
                                &dbStore,
                                CERT_QUERY_CONTENT_FLAG_PKCS7_SIGNED,
                                CERT_QUERY_FORMAT_FLAG_BINARY,
                                0,
                                NULL,
                                NULL,
                                NULL,
                                phCertStore,
                                NULL,
                                NULL))
{
    dwSts = GetLastError();
}
```

### <a name="span-idwriteoperationsspanspan-idwriteoperationsspanspan-idwriteoperationsspanwrite-operations"></a><span id="Write_operations"></span><span id="write_operations"></span><span id="WRITE_OPERATIONS"></span>写入操作

```ManagedCPlusPlus
// Serialize the store

if (FALSE == CertSaveStore( hCertStore,
                            PKCS_7_ASN_ENCODING | X509_ASN_ENCODING,
                            CERT_STORE_SAVE_AS_PKCS7,
                            CERT_STORE_SAVE_TO_MEMORY,
                            &dbStore,
                            0))
{
    dwSts = GetLastError();
    goto Ret;
}

dbStore.pbData = CspAllocH(dbStore.cbData);

if (NULL == dbStore.pbData)
{
    dwSts = ERROR_NOT_ENOUGH_MEMORY;
    goto Ret;
}

if (FALSE == CertSaveStore( hCertStore,
                            PKCS_7_ASN_ENCODING | X509_ASN_ENCODING,
                            CERT_STORE_SAVE_AS_PKCS7,
                            CERT_STORE_SAVE_TO_MEMORY,
                            &dbStore,
                            0))
{
    dwSts = GetLastError();
    goto Ret;
}
```

## <a name="span-idgrouppolicysettingsformicrosoftbasesmartcardcspspanspan-idgrouppolicysettingsformicrosoftbasesmartcardcspspanspan-idgrouppolicysettingsformicrosoftbasesmartcardcspspangroup-policy-settings-for-microsoft-base-smart-card-csp"></a><span id="Group_Policy_Settings_for_Microsoft_Base_Smart_Card_CSP"></span><span id="group_policy_settings_for_microsoft_base_smart_card_csp"></span><span id="GROUP_POLICY_SETTINGS_FOR_MICROSOFT_BASE_SMART_CARD_CSP"></span>Microsoft 基本智能卡 CSP 的组策略设置


Microsoft 基本智能卡加密服务提供程序的组策略设置位于\[HKEY\_本地\_机\\软件\\Microsoft\\加密\\默认情况下\\提供程序\\Microsoft 基本智能卡加密提供程序\]。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">键</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">DefaultPrivateKeyLenBits</td>
<td align="left"><p>dword:00000400</p>
<p>默认密钥生成参数-1024年位密钥。</p></td>
</tr>
<tr class="even">
<td align="left">RequireOnCardPrivateKeyGen</td>
<td align="left"><p>dword:00000000</p>
<p>此设置要求卡上的专用密钥生成 （默认值） 进行的标志。 如果设置此值，在主机生成的密钥可导入卡。 这用于不支持在卡生成密钥或密钥托管是必需的卡。</p></td>
</tr>
<tr class="odd">
<td align="left">TransactionTimeoutMilliseconds</td>
<td align="left"><p>dword:000005dc</p>
<p>1500，1.5 秒是用于保存到卡的事务的默认超时值。</p></td>
</tr>
<tr class="even">
<td align="left">AllowPrivateSignatureKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>允许导入签名密钥，即密钥存档方案。</p></td>
</tr>
<tr class="odd">
<td align="left">AllowPrivateExchangeKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>允许导入 exchange 密钥，即密钥存档方案。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idgrouppolicysettingsformicrosoftcngsmartcardkspspanspan-idgrouppolicysettingsformicrosoftcngsmartcardkspspanspan-idgrouppolicysettingsformicrosoftcngsmartcardkspspan-group-policy-settings-for-microsoft-cng-smart-card-ksp"></a><span id="_Group_Policy_Settings_for_Microsoft_CNG_Smart_Card_KSP"></span><span id="_group_policy_settings_for_microsoft_cng_smart_card_ksp"></span><span id="_GROUP_POLICY_SETTINGS_FOR_MICROSOFT_CNG_SMART_CARD_KSP"></span> Microsoft CNG 智能卡 KSP 的组策略设置


Microsoft CNG 智能卡密钥存储提供程序的组策略设置位于\[HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\加密\\提供程序\\Microsoft 智能卡密钥存储提供程序\]。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">键</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">DefaultPrivateKeyLenBits</td>
<td align="left"><p>dword:00000400</p>
<p>默认密钥生成参数-1024年位密钥。</p></td>
</tr>
<tr class="even">
<td align="left">RequireOnCardPrivateKeyGen</td>
<td align="left"><p>dword:00000000</p>
<p>此设置要求卡上的专用密钥生成 （默认值） 进行的标志。 如果设置此值，在主机生成的密钥可导入卡。 这用于不支持在卡生成密钥或密钥托管是必需的卡。</p></td>
</tr>
<tr class="odd">
<td align="left">TransactionTimeoutMilliseconds</td>
<td align="left"><p>dword:000005dc</p>
<p>1500，1.5 秒是用于保存到卡的事务的默认超时值。</p></td>
</tr>
<tr class="even">
<td align="left">AllowPrivateSignatureKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>允许导入签名密钥，即密钥存档方案。</p></td>
</tr>
<tr class="odd">
<td align="left">AllowPrivateExchangeKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>允许导入 exchange 密钥，即密钥存档方案。</p></td>
</tr>
<tr class="even">
<td align="left">AllocPrivateECDHEKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>允许导入 ECDH 密钥，即密钥存档方案</p></td>
</tr>
<tr class="odd">
<td align="left">AllowPrivateECDSAKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>允许导入 ECDSA 密钥，即密钥存档方案</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idspecialconsiderationsspanspan-idspecialconsiderationsspanspan-idspecialconsiderationsspanspecial-considerations"></a><span id="Special_Considerations"></span><span id="special_considerations"></span><span id="SPECIAL_CONSIDERATIONS"></span>特别注意的事项


-   在 Windows Vista Service Pack 1 (SP1) 中，在安全模式下运行的操作系统时不需要 PIN 的智能卡操作是可能的不是 Windows logon。
-   使用以下值之一调用 CryptAcquireContext 标志会提示你输入 PIN 与用户的身份验证\_而不考虑实际分配给容器的 PIN 的 PIN:

    -   CRYPT\_NEWKEYSET
    -   CRYPT\_默认\_容器\_可选
    -   CRYPT\_DELETEKEYSET
    -   CRYPT\_VERIFYCONTEXT
-   [**CardDeleteContext** ](https://docs.microsoft.com/previous-versions/dn468715(v=vs.85))甚至后可以调用*DllMain*调用时使用 DLL\_过程\_分离。

 

 

