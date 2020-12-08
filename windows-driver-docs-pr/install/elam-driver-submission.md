---
title: ELAM 驱动程序提交过程
description: 可以使用列出的步骤提交 () ELAM 的早期启动反恶意软件，以确保验证并遵守文档要求
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 881717dc60abd35167a4aa61adad3d8502bfebe0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836970"
---
# <a name="elam-driver-submission-process"></a>ELAM 驱动程序提交过程

以下步骤可用于提交 (ELAM) 驱动程序的早期启动反恶意软件：

1. 确保你的驱动程序符合 ELAM 驱动程序的记录要求。  有关详细信息，请参阅 [ELAM driver 要求](elam-driver-requirements.md) 和 [INF SignatureAttributes 部分](inf-signatureattributes-section.md) 。

2. 使用硬件徽标套件 (HLK) 和硬件认证工具包 (HCK) 来验证驱动程序。 如果你的驱动程序将在 Windows 8 和 Windows 10 中使用，则需要运行这两个版本的工具包。 将结果包含在提交的结果中。 有关详细信息，请参阅 [HLK 工具技术参考](/windows-hardware/test/hlk/user/hlk-tools-technical-reference) 。 有关所需 HCK 测试的信息，请参阅下文。

3. 如 [驱动程序签名策略](./kernel-mode-code-signing-policy--windows-vista-and-later-.md) 主题中所述，遵循内核模式驱动程序签名策略。

4. 在[Windows 硬件开发人员中心](https://developer.microsoft.com/windows)提交用于评估的驱动程序包

每个驱动程序 .sys 文件都必须是由 Microsoft 签署的代码，并使用特殊的证书指示它是一个提前的启动 AM 驱动程序。

AM 驱动程序必须是单个二进制 (不会导入任何其他 Dll) 。

## <a name="hardware-certification-kit-tests"></a>硬件认证工具包测试


针对 Windows 10 之前的操作系统的每个驱动程序都必须通过 ISV 管理的以下 HCK 测试：

性能测试
-   回拨延迟-需要每个早期启动 AM 驱动程序从5ms 中的内核返回驱动程序验证回调。 此时间是从内核向驱动程序返回回调的时间发出对驱动程序的回调时开始计算的。
-   内存分配-需要每个早期启动 AM 驱动程序将内存占用量限制为 128 KB，同时为驱动程序映像和配置 (签名) 数据。
-   卸载阻止-每个早期启动 AM 驱动程序在初始化上一个启动驱动程序后收到同步回拨，这表示将卸载 AM 驱动程序。 AM 驱动程序可以将此作为指示，它需要执行 "清理" 并保存可由运行时 AM 驱动程序使用的任何状态信息。 但是，早期启动 AM 驱动程序必须为要卸载的驱动程序返回回调，然后才能继续启动。
-   签名数据测试-每个早期启动 AM 驱动程序都必须从一个众所周知的位置获取其恶意软件签名数据，而不是其他位置。 这允许 Windows 度量和保护该数据。 此测试可确保每个 AM 驱动程序只从为该驱动程序创建的注册表配置单元中读取其配置数据。
-   备份驱动程序测试-在安装时，早期启动 AM 驱动程序还必须在备份驱动程序存储区中安装驱动程序的备份副本。 此要求用于在主驱动程序损坏的情况下帮助进行修正。 此测试可确保，对于已安装的早期启动 AM 驱动程序，备份存储中会有相应的驱动程序。
