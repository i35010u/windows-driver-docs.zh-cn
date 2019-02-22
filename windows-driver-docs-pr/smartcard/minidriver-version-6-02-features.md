---
title: 微型驱动程序版本 6.02 功能
description: 微型驱动程序版本 6.02 功能
ms.assetid: 8BF4B63B-B723-4899-BCAF-7826FAFF2155
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4c7c80de36691644eae17970dcf7481d8489dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542013"
---
# <a name="minidriver-version-602-features"></a>微型驱动程序版本 6.02 功能


在此版本中引入以下功能。

## <a name="span-idenhancedsupportforpinsspanspan-idenhancedsupportforpinsspanspan-idenhancedsupportforpinsspanenhanced-support-for-pins"></a><span id="Enhanced_Support_for_PINs"></span><span id="enhanced_support_for_pins"></span><span id="ENHANCED_SUPPORT_FOR_PINS"></span>增强了对 Pin 支持


智能卡微型驱动程序规范版本 6 增强了对 Pin 支持。 此版本引入了逻辑的固定对象的一个新概念。 开发人员可以使用 PIN 对象体系结构以控制 PIN 提示在 Windows 中并启用一组灵活且宽的方案。 PIN 对象可能会或可能不对应于在卡上的实际物理 PIN 和应被视为卡微型驱动程序以控制 PIN 相关的行为在 Windows 中一种方法。

通过一组新的 Api，卡微型驱动程序开发人员现在可以：

-   支持使用 （最多总共 8 Pin) 的 2 个以上 Pin 的卡。
-   返回到 Windows 而不是实际的 PIN 的缓存会话 PIN。
-   控制哪些字符串向用户显示期间 PIN 提示。
-   指示到 Windows 可以请求特定的键时提示输入 PIN。
-   允许访问卡或容器，而无需 PIN 提示 (空 PIN)。

有关详细信息，请参阅中的"增强型 PIN 支持"部分[开发人员准则](developer-guidelines.md)。

有关参考信息，请参阅[卡 PIN 操作](card-pin-operations.md)。

此版本中添加了新的 Api 包括：

-   [**CardAuthenticateEx**](https://msdn.microsoft.com/library/windows/hardware/dn468703)
-   [**CardGetChallengeEx**](https://msdn.microsoft.com/library/windows/hardware/dn468724)
-   [**CardDeauthenticateEx**](https://msdn.microsoft.com/library/windows/hardware/dn468713)
-   [**CardChangeAuthenticatorEx**](https://msdn.microsoft.com/library/windows/hardware/dn468706)

**重要**  不是所有预配系统支持多个 Pin; 因此，必须将应用上可以预配系统卡字段中更新的密钥的插针时格外小心。

 

## <a name="span-idsupportforread-onlycardsspanspan-idsupportforread-onlycardsspanspan-idsupportforread-onlycardsspansupport-for-read-only-cards"></a><span id="Support_for_Read-Only_Cards"></span><span id="support_for_read-only_cards"></span><span id="SUPPORT_FOR_READ-ONLY_CARDS"></span>对只读的卡的支持


安全 PIN 通道是 Windows Vista Service Pack 1 (SP1)，使安全 PIN 提示跟 Windows 与智能卡进行 PIN 身份验证之间建立安全通道中的功能。 安全 PIN 通道可防止窃听旅行通过操作系统组件和传输到卡过程时卡 PIN。

安全 PIN 提示意味着用户已请求按 ALT + CTL + DEL 前系统提示你输入 PIN 遵循与 Windows 登录相同的视觉体验。 安全 PIN 提示，可降低风险 PIN 搜集由欺骗 PIN 提示对话框框。

安全 PIN 通道可以控制并触发通用标准组策略设置，也可以通过 PIN 对象上的特定属性。

安全 PIN 通道的详细信息，请参阅中的"会话 Pin"一节[开发人员准则](developer-guidelines.md)。

与此功能相关的新 API 包括[ **CardAuthenticateEx**](https://msdn.microsoft.com/library/windows/hardware/dn468703)。

## <a name="span-idexternalpinsupportspanspan-idexternalpinsupportspanspan-idexternalpinsupportspan-external-pin-support"></a><span id="_External_PIN_Support"></span><span id="_external_pin_support"></span><span id="_EXTERNAL_PIN_SUPPORT"></span> 外部 PIN 支持


外部 PIN 支持是从用户收集关闭 PC 的 PIN。 外部 PIN 方案的示例包括：

-   PIN 收集 PIN PAD 读取器。
-   智能卡具有指纹读取器附加到它，并作为 PIN 的替代方法对卡与指纹模板执行匹配项。

在外部 PIN 模式下，每当对智能卡进行 PIN 身份验证是必需的 Windows 不会提示用户输入 PIN，但而不是调用立即而无需任何通知该用户的微型驱动程序的身份验证 API。 应不操作系统参与发生了实际的身份验证和 PIN 收集。

（可选），并根据特定限制，微型驱动程序允许显示其自身用户界面 (UI) 以指示用户执行与 PIN 收集的关系中的特定操作。 不应这样的用户界面用于实际从用户收集 PIN 而不是 Windows 正在等待外部收集使用 PIN 将用户定向。 不允许微型驱动程序时要显示用户界面上下文是静默模式下，应使用特定的窗口句柄创建 UI 元素。 中可以找到更多信息[ **CardAuthenticateEx**](https://msdn.microsoft.com/library/windows/hardware/dn468703)，并[ **CardSetProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468740)。

可以返回临时会话 PIN 的卡可能会返回此类固定到 Windows 以进行后续缓存。 在这种情况下，Windows 提供了会话 PIN 进行任何进一步卡身份验证，直到卡使会话 PIN 无效。 有关详细信息，请参阅[ **CardAuthenticateEx**](https://msdn.microsoft.com/library/windows/hardware/dn468703)。

 

 





