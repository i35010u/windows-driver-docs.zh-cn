---
title: 开发人员指南
description: 本主题讨论使用和开发智能卡微型驱动程序的一般准则。
ms.assetid: 48999DF6-3AC2-4DEA-8ABC-C427237B31E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b454f32f7db161d62d8b1f4bad5714656601e0d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101634"
---
# <a name="developer-guidelines"></a>开发人员指南


本主题讨论了使用和/或开发智能卡微型驱动程序的开发人员的一般准则，让你了解智能卡及其关联应用程序的预期行为。

## <a name="span-idgeneral_design_guidelinesspanspan-idgeneral_design_guidelinesspanspan-idgeneral_design_guidelinesspangeneral-design-guidelines"></a><span id="General_Design_Guidelines"></span><span id="general_design_guidelines"></span><span id="GENERAL_DESIGN_GUIDELINES"></span>一般设计准则


有关如何分发卡微型驱动程序、如何映射逻辑卡文件系统和其他微型驱动程序设计准则的信息，请参阅 "[智能卡微型驱动程序概述](smart-card-minidriver-overview.md)" 下的 "**常规设计指南**" 部分。

## <a name="span-idchallenge_response_method_of_unblocking_smart_card_pinspanspan-idchallenge_response_method_of_unblocking_smart_card_pinspanspan-idchallenge_response_method_of_unblocking_smart_card_pinspanchallengeresponse-method-of-unblocking-smart-card-pin"></a><span id="Challenge_Response_Method_of_Unblocking_Smart_Card_PIN"></span><span id="challenge_response_method_of_unblocking_smart_card_pin"></span><span id="CHALLENGE_RESPONSE_METHOD_OF_UNBLOCKING_SMART_CARD_PIN"></span>阻止智能卡 PIN 的质询/响应方法


为了使管理员能够成功地取消阻止用户的卡，管理员必须能够识别和使用存储在卡上的管理员密钥，以使他们能够正确地为发出的质询生成响应数据。

实现此目的的一种方法是使用卡标识符来唯一地标识该卡。  (卡标识符是卡的唯一标识符。 ) 这可以用某种形式表示给 UI 中的用户，但也可以将程序编写为将相应的 APDU 命令发送到卡，以读取此信息。

然后，此信息可让管理员识别卡上的密钥，并计算对向用户颁发的质询数据的适当响应。

假设卡上存储的管理员密钥通过使用某些安全机制持有，该机制仅适用于有效的受信任管理员 (最好尽可能少地) 。 但这超出了本规范的范畴。

有关详细信息，请参阅以下 "质询/响应机制" 一节。

## <a name="span-idenhanced_pin_supportspanspan-idenhanced_pin_supportspanspan-idenhanced_pin_supportspanenhanced-pin-support"></a><span id="Enhanced_PIN_Support"></span><span id="enhanced_pin_support"></span><span id="ENHANCED_PIN_SUPPORT"></span>增强的 PIN 支持


版本6.0 支持为多个 PIN 支持提供灵活的体系结构。 此体系结构引入了一个新的角色概念，其中每个角色对应于一个 PIN 标识符。 PIN 标识符用于从智能卡中提取 PIN 信息，并将 PIN 与密钥容器关联。

标识符由数字组成，当前限制为 0 through7。 还介绍了 PIN 集的概念 \_ ，这是一个可从 pin 标识符生成的位掩码。 目前仅将较低的8位用于 PIN 集。 我们还可以选择使用剩余的位数来指示诸如 "和"、"或" 之类的条件，或者我们在将来可能会发现有用的其他信息。 我们选择了此方法，以便可以轻松地将位掩码用于实现。

假设用户在与 PIN 3 对应的角色3中进行身份验证 \# 。 这会转换为位掩码 0000 0100 (base 2) 。 智能卡可以将其记录为当前经过身份验证的 ID，并可通过执行逐位和操作轻松验证密钥和 Pin 的访问控制规则。 该设计允许同时在卡片上具有多个已验证的标识，这是支持 v6 卡微型驱动程序的卡的要求。 例如，如果先对 PIN \# 1 进行身份验证，然后对 pin \# 2 进行身份验证，则应允许任何这些 pin 控制的操作。

## <a name="span-id_session_pins_and_secure_pin_channelspanspan-id_session_pins_and_secure_pin_channelspanspan-id_session_pins_and_secure_pin_channelspan-session-pins-and-secure-pin-channel"></a><span id="_Session_PINs_and_Secure_PIN_Channel"></span><span id="_session_pins_and_secure_pin_channel"></span><span id="_SESSION_PINS_AND_SECURE_PIN_CHANNEL"></span> 会话 Pin 和安全 PIN 通道


当 Windows 必须建立用于 PIN 身份验证的安全 PIN 通道时，将使用微型驱动程序执行以下序列操作。 若要符合，微型驱动程序和卡必须与以下顺序兼容。 特别是，会话 Pin 应该在进程之间进行转移，并且仅在特定的时间段内进行。  (建议在使用卡进行身份验证会话 pin 标志之前，任何会话 PIN 都有效， \_ 即使使用 \_ \_ "生成会话 pin 标志" 设置调用 [**CardAuthenticateEx**](/previous-versions/dn468703(v=vs.85)) \_ \_ 。 ) 

应支持以下行为：

1.  应用程序 A （一个受信任的系统进程）获取智能卡的句柄并收集 PIN。
2.  然后，应用程序 A 调用卡 [**CardAuthenticateEx**](/previous-versions/dn468703(v=vs.85)) 微型驱动程序函数，传递收集的 PIN，并设置卡 \_ 身份验证 \_ 生成 \_ 会话 \_ PIN 标志。 这不会导致卡解锁。
3.  应用程序 A 存储已生成的会话 PIN，并释放卡和卡微型驱动程序的句柄。 该卡不是冷重置。
4.  应用程序 A 将会话 PIN 和在步骤1中获得的读卡器的名称发送到应用程序 B。
5.  应用程序 B 获取与1中相同的卡。
6.  应用程序 B 调用 [**CardAuthenticateEx**](/previous-versions/dn468703(v=vs.85)) 并传入会话 pin，并设置卡 \_ 身份验证 \_ 会话 \_ pin 标志。 如果会话 PIN 仍然有效，则应对卡进行身份验证并有效地使用。
7.  当应用程序 B 使用完该卡后，它会调用 [**CardDeauthenticateEx**](/previous-versions/dn468713(v=vs.85)) deauthorize 卡。

此行为具有以下实际限制：

-   卡必须通过返回适用于 CP \_ 卡 \_ PIN \_ 强度验证的相应值声明其使用会话 pin 的能力 \_ 。
-   依赖于每个验证的 PIN 的卡不能与此系统兼容。
-   几个应用程序可以在任何时候将其确定为有效会话 Pin。 如果每个 PIN 只能有一个会话 PIN，则建议以下实现：

    -   该卡应记得生成的最新会话 PIN。
    -   如果提供的会话 PIN 无效，则该卡应该会导致身份验证失败，并在支持时减少会话 PIN 的重试计数器。 如果重试计数达到0，并且下一次身份验证尝试无效，则会话 PIN 应失效。
    -   在协商新的会话 PIN 之前，后续会话 PIN 演示文稿应该会失败。
-   必须能够从系统上的不同应用程序使用会话 PIN。
-   会话 PIN 不得简单地是 PIN 编码。
-   此系统的安全性仅限于会话 PIN 的强度和用于生成它的协商协议。 实际会话 PIN 协商超出了本规范的范围。 除了此部分中所述，我们对设计没有要求。
-   会话 PIN 仍被视为重要，应视为机密。
-   该卡应该能够检测到无效的会话 PIN。

## <a name="span-idread-only_cardsspanspan-idread-only_cardsspanspan-idread-only_cardsspanread-only-cards"></a><span id="Read-Only_Cards"></span><span id="read-only_cards"></span><span id="READ-ONLY_CARDS"></span>只读卡


若要对在基本 CSP/KSP 环境之外个性化的卡进行寻址，并且本质上是只读的，我们引入了只读卡的新概念。 如果卡是只读的，则它必须通过 [**CardGetProperty**](/previous-versions/dn468729(v=vs.85)) 函数播发此内容， (在此规范) 之前查看此部分。

只读卡必须仅支持版本7卡微型驱动程序接口的子集，并且无需支持管理员 PIN。

下表列出了只读卡必须支持的函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数名称</th>
<th align="left">必须</th>
<th align="left">注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468701(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAcquireContext&lt;/strong&gt;](/previous-versions/dn468701(v=vs.85))"><strong>CardAcquireContext</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468715(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteContext&lt;/strong&gt;](/previous-versions/dn468715(v=vs.85))"><strong>CardDeleteContext</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468704(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAuthenticatePin&lt;/strong&gt;](/previous-versions/dn468704(v=vs.85))"><strong>CardAuthenticatePin</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468723(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetChallenge&lt;/strong&gt;](/previous-versions/dn468723(v=vs.85))"><strong>CardGetChallenge</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468702(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAuthenticateChallenge&lt;/strong&gt;](/previous-versions/dn468702(v=vs.85))"><strong>CardAuthenticateChallenge</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468712(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeauthenticate&lt;/strong&gt;](/previous-versions/dn468712(v=vs.85))"><strong>CardDeauthenticate</strong></a></td>
<td align="left">是 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468742(v=vs.85)" data-raw-source="[&lt;strong&gt;CardUnblockPin&lt;/strong&gt;](/previous-versions/dn468742(v=vs.85))"><strong>CardUnblockPin</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468705(v=vs.85)" data-raw-source="[&lt;strong&gt;CardChangeAuthenticator&lt;/strong&gt;](/previous-versions/dn468705(v=vs.85))"><strong>CardChangeAuthenticator</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468710(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateDirectory&lt;/strong&gt;](/previous-versions/dn468710(v=vs.85))"><strong>CardCreateDirectory</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468716(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](/previous-versions/dn468716(v=vs.85))"><strong>CardDeleteDirectory</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468736(v=vs.85)" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](/previous-versions/dn468736(v=vs.85))"><strong>CardReadFile</strong></a></td>
<td align="left">是</td>
<td align="left">卡微型驱动程序必须模拟文件系统。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468711(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](/previous-versions/dn468711(v=vs.85))"><strong>CardCreateFile</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468727(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetFileInfo&lt;/strong&gt;](/previous-versions/dn468727(v=vs.85))"><strong>CardGetFileInfo</strong></a></td>
<td align="left">是</td>
<td align="left">卡微型驱动程序必须模拟文件系统。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468743(v=vs.85)" data-raw-source="[&lt;strong&gt;CardWriteFile&lt;/strong&gt;](/previous-versions/dn468743(v=vs.85))"><strong>CardWriteFile</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468711(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteFile&lt;/strong&gt;](/previous-versions/dn468711(v=vs.85))"><strong>CardDeleteFile</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468721(v=vs.85)" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](/previous-versions/dn468721(v=vs.85))"><strong>CardEnumFiles</strong></a></td>
<td align="left">是</td>
<td align="left">卡微型驱动程序必须模拟文件系统。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468734(v=vs.85)" data-raw-source="[&lt;strong&gt;CardQueryFreeSpace&lt;/strong&gt;](/previous-versions/dn468734(v=vs.85))"><strong>CardQueryFreeSpace</strong></a></td>
<td align="left">是</td>
<td align="left">卡微型驱动程序必须模拟文件系统。</td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468733(v=vs.85)" data-raw-source="[&lt;strong&gt;CardQueryCapabilities&lt;/strong&gt;](/previous-versions/dn468733(v=vs.85))"><strong>CardQueryCapabilities</strong></a></td>
<td align="left">是</td>
<td align="left">卡微型驱动程序必须模拟文件系统。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468708(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateContainer&lt;/strong&gt;](/previous-versions/dn468708(v=vs.85))"><strong>CardCreateContainer</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468709(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateContainerEx&lt;/strong&gt;](/previous-versions/dn468709(v=vs.85))"><strong>CardCreateContainerEx</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468714(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteContainer&lt;/strong&gt;](/previous-versions/dn468714(v=vs.85))"><strong>CardDeleteContainer</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468725(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetContainerInfo&lt;/strong&gt;](/previous-versions/dn468725(v=vs.85))"><strong>CardGetContainerInfo</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468737(v=vs.85)" data-raw-source="[&lt;strong&gt;CardRSADecrypt&lt;/strong&gt;](/previous-versions/dn468737(v=vs.85))"><strong>CardRSADecrypt</strong></a></td>
<td align="left">是 (可选) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468707(v=vs.85)" data-raw-source="[&lt;strong&gt;CardConstructDHAgreement&lt;/strong&gt;](/previous-versions/dn468707(v=vs.85))"><strong>CardConstructDHAgreement</strong></a></td>
<td align="left">是 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468718(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeriveKey&lt;/strong&gt;](/previous-versions/dn468718(v=vs.85))"><strong>CardDeriveKey</strong></a></td>
<td align="left">是 (可选) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468719(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDestroyDHAgreement&lt;/strong&gt;](/previous-versions/dn468719(v=vs.85))"><strong>CardDestroyDHAgreement</strong></a></td>
<td align="left">是 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468741(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSignData&lt;/strong&gt;](/previous-versions/dn468741(v=vs.85))"><strong>CardSignData</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468735(v=vs.85)" data-raw-source="[&lt;strong&gt;CardQueryKeySizes&lt;/strong&gt;](/previous-versions/dn468735(v=vs.85))"><strong>CardQueryKeySizes</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468703(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAuthenticateEx&lt;/strong&gt;](/previous-versions/dn468703(v=vs.85))"><strong>CardAuthenticateEx</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468706(v=vs.85)" data-raw-source="[&lt;strong&gt;CardChangeAuthenticatorEx&lt;/strong&gt;](/previous-versions/dn468706(v=vs.85))"><strong>CardChangeAuthenticatorEx</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468713(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeauthenticateEx&lt;/strong&gt;](/previous-versions/dn468713(v=vs.85))"><strong>CardDeauthenticateEx</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468724(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetChallengeEx&lt;/strong&gt;](/previous-versions/dn468724(v=vs.85))"><strong>CardGetChallengeEx</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468726(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetContainerProperty&lt;/strong&gt;](/previous-versions/dn468726(v=vs.85))"><strong>CardGetContainerProperty</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468738(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSetContainerProperty&lt;/strong&gt;](/previous-versions/dn468738(v=vs.85))"><strong>CardSetContainerProperty</strong></a></td>
<td align="left">否</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468729(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetProperty&lt;/strong&gt;](/previous-versions/dn468729(v=vs.85))"><strong>CardGetProperty</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468740(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSetProperty&lt;/strong&gt;](/previous-versions/dn468740(v=vs.85))"><strong>CardSetProperty</strong></a></td>
<td align="left">是</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468757(v=vs.85)" data-raw-source="[&lt;strong&gt;MDImportSessionKey&lt;/strong&gt;](/previous-versions/dn468757(v=vs.85))"><strong>MDImportSessionKey</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468756(v=vs.85)" data-raw-source="[&lt;strong&gt;MDEncryptData&lt;/strong&gt;](/previous-versions/dn468756(v=vs.85))"><strong>MDEncryptData</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468731(v=vs.85)" data-raw-source="[&lt;strong&gt;CardImportSessionKey&lt;/strong&gt;](/previous-versions/dn468731(v=vs.85))"><strong>CardImportSessionKey</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468730(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetSharedKeyHandle&lt;/strong&gt;](/previous-versions/dn468730(v=vs.85))"><strong>CardGetSharedKeyHandle</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468722(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetAlgorithmProperty&lt;/strong&gt;](/previous-versions/dn468722(v=vs.85))"><strong>CardGetAlgorithmProperty</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468728(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetKeyProperty&lt;/strong&gt;](/previous-versions/dn468728(v=vs.85))"><strong>CardGetKeyProperty</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468739(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSetKeyProperty&lt;/strong&gt;](/previous-versions/dn468739(v=vs.85))"><strong>CardSetKeyProperty</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="/previous-versions/dn468720(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDestroyKey&lt;/strong&gt;](/previous-versions/dn468720(v=vs.85))"><strong>CardDestroyKey</strong></a></td>
<td align="left">无 (可选) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="/previous-versions/dn468732(v=vs.85)" data-raw-source="[&lt;strong&gt;CardProcessEncryptedData&lt;/strong&gt;](/previous-versions/dn468732(v=vs.85))"><strong>CardProcessEncryptedData</strong></a></td>
<td align="left">无 (可选) </td>
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
<td align="left">入口点必须存在并且必须返回 SCARD_E_UNSUPPORTED_FEATURE。</td>
</tr>
<tr class="odd">
<td align="left">无 (可选) </td>
<td align="left">只读卡不需要此操作，但如果卡支持该操作，则可能实现该操作。 如果不支持，入口点必须返回 SCARD_E_UNSUPPORTED_FEATURE。</td>
</tr>
<tr class="even">
<td align="left">是 (可选) </td>
<td align="left">应根据此规范中的定义来实现此函数，而不考虑卡是否为只读。</td>
</tr>
</tbody>
</table>

 

在为只读卡开发微型驱动程序时，应考虑以下要求：

-   除 "msroots" 文件 (（例如 "cardcf" 和 "cardid ) "）以外，所有预期的基本 CSP/KSP 文件都必须位于只读卡 (上，或者必须通过微型驱动程序接口) 进行虚拟化。
-   只读卡必须包含至少一个由主卡保护的卡上的密钥， (为角色 \_ 用户) PIN。
-   允许只读卡不包含管理密钥。 如果出现这种情况，则微型驱动程序将不支持 [**CardGetChallenge**](/previous-versions/dn468723(v=vs.85))、 [**CardAuthenticateChallenge**](/previous-versions/dn468702(v=vs.85))和 [**CardUnblockPin**](/previous-versions/dn468742(v=vs.85))。
-   查询时，只读卡应返回可用的0字节和0个容器。
-   只 \_ \_ \_ \_ \_ 允许在只读卡上设置 cp 父窗口和 cp 固定上下文字符串属性。
-   对于只读卡，CP \_ 支持 \_ WIN \_ X509 \_ 注册属性应为 false。

## <a name="span-idcache_modesspanspan-idcache_modesspanspan-idcache_modesspancache-modes"></a><span id="Cache_Modes"></span><span id="cache_modes"></span><span id="CACHE_MODES"></span>缓存模式


基本 CSP/KSP 支持三种不同的缓存模式，具体取决于使用参数 CP [**CardGetProperty**](/previous-versions/dn468729(v=vs.85)) \_ 卡 \_ 缓存模式调用的 CardGetProperty 返回的缓存模式 \_ ：

-   如果返回的标志为 CP \_ 缓存 \_ 模式 \_ 全局 \_ 缓存，并且该卡将 CP \_ 只读 \_ \_ 卡属性报告为 TRUE，则基本 CSP/KSP 数据缓存是全局缓存。 如果卡是只读的，则基本 CSP/KSP 不会写入 cardcf 文件。 如果可以将该卡写入基本 CSP/KSP，则它将按今天的方式运行。
-   有关 CP \_ 卡 \_ 缓存 \_ 模式和 cp \_ 缓存 \_ 模式全局缓存的详细信息 \_ \_ ，请参阅 [**CardGetProperty**](/previous-versions/dn468729(v=vs.85))。
-   如果返回的标志仅为 CP \_ 缓存 \_ 模式 \_ 会话 \_ ，则基本 CSP/KSP 将运行，以便在检测到已删除或重新插入卡时清除数据缓存。 换句话说，我们已将会话定义为插入和删除卡之间的跨度。
-   还会为每个进程实现缓存，而不是全局缓存。 此模式适用于在用户的电脑上不会更改的只读卡，而是在某些政府工作站或其他外部站点。 对于读/写卡 (此模式，但建议对这些卡采用全局缓存。 ) 
-   如果卡是只读的，并且可能会在用户的 PC 上更改卡， (方法是使用基础 CSP/KSP) 以外的其他方式），则应用程序应使用本规范稍后部分中描述的 "无缓存" 模式，以避免缓存中包含过时数据的情况。
-   如果标志为 CP \_ 缓存 \_ 模式 \_ NO \_ CACHE，则基本 CSP/KSP 不实现任何数据缓存。 此模式适用于不支持写入 cardcf 文件，但卡片状态可以更改的卡微型驱动程序。 卡微型驱动程序决定是否要在其层中执行任何缓存。

## <a name="span-id_challenge_response_mechanismspanspan-id_challenge_response_mechanismspanspan-id_challenge_response_mechanismspan-challengeresponse-mechanism"></a><span id="_Challenge_Response_Mechanism"></span><span id="_challenge_response_mechanism"></span><span id="_CHALLENGE_RESPONSE_MECHANISM"></span> 质询/响应机制


卡微型驱动程序接口支持质询/响应身份验证机制。 卡必须生成一个或多个8字节块的质询。 身份验证实体通过使用在 CBC 模式下操作的三重 DES (3DES) 来计算响应，该在具有168位密钥 (并忽略奇偶校验位) 上操作。

卡使用以下方法之一验证响应：

-   对以前发出的质询重复执行加密操作并比较结果。
-   解密响应并将结果与质询进行比较。

如果生成的值相同，则身份验证成功。

卡和身份验证实体都必须使用相同的对称密钥。

下面的示例代码详细说明了身份验证实体如何计算响应。 此代码不包含任何关联的担保，仅作为一个示例和指导提供。

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

## <a name="span-id_interoperability_with_msrootsspanspan-id_interoperability_with_msrootsspanspan-id_interoperability_with_msrootsspan-interoperability-with-msroots"></a><span id="_Interoperability_with_msroots"></span><span id="_interoperability_with_msroots"></span><span id="_INTEROPERABILITY_WITH_MSROOTS"></span> 与 msroots 的互操作性


Msroots 文件是 \# 适用于企业信任的根的 PKCS 7 格式化证书存储区。  (文件是包含空内容的一袋证书和一个空签名，并由基本 CSP 写入和读取。 ) 卡微型驱动程序开发人员无需在卡片微型驱动程序中编写任何特殊代码即可处理此文件。 将证书存储在 msroots 文件中时，代码 \_ 签名 EKU 等属性不会传播到智能卡，因为 msroots 文件以不同于计算机存储的格式存储证书。 如果开发人员要从其他应用程序读取或写入此文件，则可以使用以下示例代码片段来访问数据。

### <a name="span-idread_operationsspanspan-idread_operationsspanspan-idread_operationsspanread-operations"></a><span id="Read_operations"></span><span id="read_operations"></span><span id="READ_OPERATIONS"></span>读取操作

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

### <a name="span-idwrite_operationsspanspan-idwrite_operationsspanspan-idwrite_operationsspanwrite-operations"></a><span id="Write_operations"></span><span id="write_operations"></span><span id="WRITE_OPERATIONS"></span>写入操作

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

## <a name="span-idgroup_policy_settings_for_microsoft_base_smart_card_cspspanspan-idgroup_policy_settings_for_microsoft_base_smart_card_cspspanspan-idgroup_policy_settings_for_microsoft_base_smart_card_cspspangroup-policy-settings-for-microsoft-base-smart-card-csp"></a><span id="Group_Policy_Settings_for_Microsoft_Base_Smart_Card_CSP"></span><span id="group_policy_settings_for_microsoft_base_smart_card_csp"></span><span id="GROUP_POLICY_SETTINGS_FOR_MICROSOFT_BASE_SMART_CARD_CSP"></span>Microsoft 基本智能卡 CSP 组策略设置


Microsoft 基本智能卡加密服务提供程序组策略设置位于 \[ HKEY \_ 本地 \_ 计算机 \\ 软件 \\ microsoft \\ 加密 \\ 默认 \\ 提供程序 \\ microsoft 基本智能卡加密提供 \] 程序中。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">密钥</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">DefaultPrivateKeyLenBits</td>
<td align="left"><p>dword：00000400</p>
<p>默认密钥生成参数-1024 位密钥。</p></td>
</tr>
<tr class="even">
<td align="left">RequireOnCardPrivateKeyGen</td>
<td align="left"><p>dword：00000000</p>
<p>这会设置标志，要求 (默认) 上生成卡上私钥。 如果设置了此值，则可以将在主机上生成的密钥导入到卡中。 这适用于不支持卡上密钥生成的卡或需要进行密钥委托的卡。</p></td>
</tr>
<tr class="odd">
<td align="left">TransactionTimeoutMilliseconds</td>
<td align="left"><p>dword：000005dc</p>
<p>1500，1.5 秒是在卡上保存事务的默认超时值。</p></td>
</tr>
<tr class="even">
<td align="left">AllowPrivateSignatureKeyImport</td>
<td align="left"><p>dword：00000000</p>
<p>允许导入签名密钥，即密钥存档方案。</p></td>
</tr>
<tr class="odd">
<td align="left">AllowPrivateExchangeKeyImport</td>
<td align="left"><p>dword：00000000</p>
<p>允许导入 exchange 密钥，即密钥存档方案。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-id_group_policy_settings_for_microsoft_cng_smart_card_kspspanspan-id_group_policy_settings_for_microsoft_cng_smart_card_kspspanspan-id_group_policy_settings_for_microsoft_cng_smart_card_kspspan-group-policy-settings-for-microsoft-cng-smart-card-ksp"></a><span id="_Group_Policy_Settings_for_Microsoft_CNG_Smart_Card_KSP"></span><span id="_group_policy_settings_for_microsoft_cng_smart_card_ksp"></span><span id="_GROUP_POLICY_SETTINGS_FOR_MICROSOFT_CNG_SMART_CARD_KSP"></span> Microsoft CNG 智能卡 KSP 组策略设置


Microsoft CNG 智能卡密钥存储提供程序组策略设置位于 \[ HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Control \\ 密码提供程序 \\ \\ Microsoft 智能卡密钥存储提供程序中 \] 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">密钥</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">DefaultPrivateKeyLenBits</td>
<td align="left"><p>dword：00000400</p>
<p>默认密钥生成参数-1024 位密钥。</p></td>
</tr>
<tr class="even">
<td align="left">RequireOnCardPrivateKeyGen</td>
<td align="left"><p>dword：00000000</p>
<p>这会设置标志，要求 (默认) 上生成卡上私钥。 如果设置了此值，则可以将在主机上生成的密钥导入到卡中。 这适用于不支持卡上密钥生成的卡或需要进行密钥委托的卡。</p></td>
</tr>
<tr class="odd">
<td align="left">TransactionTimeoutMilliseconds</td>
<td align="left"><p>dword：000005dc</p>
<p>1500，1.5 秒是在卡上保存事务的默认超时值。</p></td>
</tr>
<tr class="even">
<td align="left">AllowPrivateSignatureKeyImport</td>
<td align="left"><p>dword：00000000</p>
<p>允许导入签名密钥，即密钥存档方案。</p></td>
</tr>
<tr class="odd">
<td align="left">AllowPrivateExchangeKeyImport</td>
<td align="left"><p>dword：00000000</p>
<p>允许导入 exchange 密钥，即密钥存档方案。</p></td>
</tr>
<tr class="even">
<td align="left">AllocPrivateECDHEKeyImport</td>
<td align="left"><p>dword：00000000</p>
<p>允许导入 ECDH 密钥，即密钥存档方案</p></td>
</tr>
<tr class="odd">
<td align="left">AllowPrivateECDSAKeyImport</td>
<td align="left"><p>dword：00000000</p>
<p>允许导入 ECDSA 密钥，即密钥存档方案</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idspecial_considerationsspanspan-idspecial_considerationsspanspan-idspecial_considerationsspanspecial-considerations"></a><span id="Special_Considerations"></span><span id="special_considerations"></span><span id="SPECIAL_CONSIDERATIONS"></span>特别注意事项


-   在带有 Service Pack 1 (SP1) 的 Windows Vista 中，当操作系统在安全模式下运行时，不能执行 PIN 所需的智能卡操作，而不是 Windows 登录。
-   在调用 CryptAcquireContext 时，如果通过用户 pin 执行 PIN 身份验证，则 \_ 不考虑分配给容器的实际 PIN：

    -   DM-CRYPT \_ NEWKEYSET
    -   DM-CRYPT \_ 默认 \_ 容器（ \_ 可选）
    -   DM-CRYPT \_ DELETEKEYSET
    -   DM-CRYPT \_ VERIFYCONTEXT
-   即使在 DLL 进程分离调用了*DllMain*后，也可以调用[**CardDeleteContext**](/previous-versions/dn468715(v=vs.85)) \_ \_ 。

