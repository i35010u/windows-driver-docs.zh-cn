---
title: 微型驱动程序版本 6.02 功能
description: 微型驱动程序版本 6.02 功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15d009d70ad4537d3b11778d1da8be7980a459e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804903"
---
# <a name="minidriver-version-602-features"></a>微型驱动程序版本 6.02 功能


此版本中引入了以下功能。

## <a name="span-idenhanced_support_for_pinsspanspan-idenhanced_support_for_pinsspanspan-idenhanced_support_for_pinsspanenhanced-support-for-pins"></a><span id="Enhanced_Support_for_PINs"></span><span id="enhanced_support_for_pins"></span><span id="ENHANCED_SUPPORT_FOR_PINS"></span>对 Pin 的增强支持


智能卡微型驱动程序规范的版本6增强了对 Pin 的支持。 此版本引入了逻辑 PIN 对象的新概念。 开发人员可以使用 PIN 对象体系结构来控制 Windows 中的 PIN 提示，并实现灵活且广泛的方案集。 PIN 对象不一定对应于卡上的实际物理 PIN，并且应作为卡微型驱动程序控制 Windows 中与 PIN 相关的行为的方式进行查看。

通过一组新的 Api，微型驱动程序的开发人员现在可以：

-   使用2个以上的 Pin 的支持卡 (的总) 最多8个 Pin。
-   将会话 PIN 返回给 Windows 以进行缓存，而不是实际的 PIN。
-   控制在 PIN 提示期间向用户显示的字符串。
-   指示在请求特定密钥时 Windows 提示输入 PIN。
-   允许在没有 PIN 提示的情况下访问卡或容器 (空 PIN) 。

有关详细信息，请参阅 [开发人员指南](developer-guidelines.md)中的 "增强 PIN 支持" 一节。

有关参考信息，请参阅 [卡针操作](card-pin-operations.md)。

在此版本中添加的新 Api 包括：

-   [**CardAuthenticateEx**](/previous-versions/dn468703(v=vs.85))
-   [**CardGetChallengeEx**](/previous-versions/dn468724(v=vs.85))
-   [**CardDeauthenticateEx**](/previous-versions/dn468713(v=vs.85))
-   [**CardChangeAuthenticatorEx**](/previous-versions/dn468706(v=vs.85))

**重要提示**  并非所有预配系统都支持多个 Pin;因此，在可通过卡预配系统将 Pin 应用于字段时，必须小心谨慎。

 

## <a name="span-idsupport_for_read-only_cardsspanspan-idsupport_for_read-only_cardsspanspan-idsupport_for_read-only_cardsspansupport-for-read-only-cards"></a><span id="Support_for_Read-Only_Cards"></span><span id="support_for_read-only_cards"></span><span id="SUPPORT_FOR_READ-ONLY_CARDS"></span>支持 Read-Only 卡


安全 PIN 通道是 Windows Vista Service Pack 1 (SP1) 中的一项功能，它启用安全 PIN 提示，然后在 Windows 与智能卡之间建立安全通道以进行 PIN 身份验证。 安全 PIN 通道保护卡 PIN 不受窃听，同时通过操作系统组件进行传播，并传输到卡。

安全 PIN 提示表示在出现与 Windows 登录相同的视觉体验之后，要求用户按 ALT + CTL + DEL。 安全 PIN 提示可降低通过欺骗 PIN 提示对话框进行 PIN 收集的风险。

安全 PIN 通道可以通过通用标准组策略设置来控制和触发，还可以通过固定对象上的特定属性进行管理。

有关安全 PIN 通道的详细信息，请参阅 [开发人员指南](developer-guidelines.md)中的 "会话 pin" 一节。

与此功能相关的新 API 包括 [**CardAuthenticateEx**](/previous-versions/dn468703(v=vs.85))。

## <a name="span-id_external_pin_supportspanspan-id_external_pin_supportspanspan-id_external_pin_supportspan-external-pin-support"></a><span id="_External_PIN_Support"></span><span id="_external_pin_support"></span><span id="_EXTERNAL_PIN_SUPPORT"></span> 外部 PIN 支持


外部 PIN 支持是指从用户那里收集的 PIN。 外部 PIN 方案的示例包括：

-   Pin 是在 PIN 板读取器上收集的。
-   智能卡上附加了指纹读取器，并使用指纹模板作为 PIN 的替代方法在卡上执行匹配。

在外部 PIN 模式下，每当需要对智能卡进行 PIN 身份验证时，Windows 不会提示用户输入 PIN，而是立即调用微型驱动程序的身份验证 API，而不会向用户发送任何通知。 实际的身份验证和 PIN 收集应发生，无需操作系统介入。

（可选）根据特定限制，允许微型驱动程序显示其自己的用户界面 (UI) ，以指示用户执行与固定集合相关的特定操作。 不应使用此类 UI 来实际收集用户的 PIN，而是指示用户 Windows 正在等待外部收集的 PIN，而不是这样。 当上下文是静默模式时，不允许微型驱动程序显示 UI，并且应使用特定窗口句柄来创建 UI 元素。 有关详细信息，请参阅 [**CardAuthenticateEx**](/previous-versions/dn468703(v=vs.85))和 [**CardSetProperty**](/previous-versions/dn468740(v=vs.85))。

可以返回临时会话 PIN 的卡可能会将此类 PIN 返回给 Windows 以进行后续缓存。 在这种情况下，Windows 会在卡使会话 PIN 失效之前为任何其他卡身份验证提供会话 PIN。 有关详细信息，请参阅 [**CardAuthenticateEx**](/previous-versions/dn468703(v=vs.85))。

 

