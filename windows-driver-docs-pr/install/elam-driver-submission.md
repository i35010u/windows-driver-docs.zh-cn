---
title: ELAM 先决条件
description: 可以使用列出的步骤来确保验证并且对有案可稽的要求的遵从性提交早期启动反恶意软件 (ELAM) 驱动程序
ms.assetid: ''
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c19c473123fab03d9077931a47a7a4c03b66594
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346147"
---
# <a name="elam-driver-submission-process"></a>ELAM 驱动程序提交过程

以下步骤可用于提交的早期启动反恶意软件 (ELAM) 驱动程序：

1. 请确保您的驱动程序符合 ELAM 驱动程序有案可稽的要求。  请参阅[ELAM 驱动程序要求](elam-driver-requirements.md)并[INF SignatureAttributes 部分](inf-signatureattributes-section.md)有关详细信息。

2. 验证您使用的硬件徽标工具包 (HLK) 和硬件认证工具包 (HCK) 的驱动程序。 如果您的驱动程序将使用在 Windows 8 和 Windows 10 中，您需要运行两个版本的工具包。 包括与您的提交结果。 请参阅[HLK 工具技术参考](https://msdn.microsoft.com/library/windows/hardware/dn939924)有关详细信息。 有关必需 HCK 测试的信息，请参阅下面。

3. 请按照内核模式驱动程序签名策略，如中所述[驱动程序签名策略](https://docs.microsoft.com/windows-hardware/drivers/install/kernel-mode-code-signing-policy--windows-vista-and-later-)主题。

4. 提交的评估的驱动程序包[Windows 硬件开发人员中心](https://developer.microsoft.com/windows)

每个驱动程序.sys 文件必须是 Microsoft，使用一个特殊的证书，该值开机初期启动 AM 驱动程序签名的代码。

AM 驱动程序必须是单一的二进制文件 （未导入任何其他 Dll）。

## <a name="hardware-certification-kit-tests"></a>硬件认证工具包测试


每个面向早于 Windows 10 操作系统的驱动程序必须通过以下的 HCK 测试由 ISV 管理：

性能测试
-   回调延迟-每个早期启动 AM 的驱动程序时需要从内核中.5ms 返回驱动程序验证回调。 这一次计从内核驱动程序添加到驱动程序返回回调时向发出回调。
-   内存分配的每个早期启动 AM 的驱动程序时需要限制为 128 KB，驱动程序映像以及其配置 （签名） 数据的内存中占用空间。
-   最后一个启动驱动程序初始化后，它指示 AM 驱动程序将被卸载，卸载阻止的每个开机初期启动的 AM 驱动程序将收到同步回调。 AM 驱动程序可以使用此来指明它需要执行"清理"，并将运行 AM 时驱动程序可以使用任何状态信息。 但是，早期启动 AM 的驱动程序必须返回回调驱动程序无法卸载和启动继续。
-   签名数据测试-每个早期启动 AM 的驱动程序必须获取从单个的已知位置和任何其他的恶意软件签名数据。 这允许度量和通过 Windows 数据保护。 此测试可确保，每个 AM 驱动程序仅读取其配置数据从创建的注册表配置单元为该驱动程序。
-   备份驱动程序测试-开机初期启动 AM 驱动程序，在安装时，还必须向备份驱动程序存储区安装驱动程序的备份副本。 此要求是帮助进行修正在主要的驱动程序获取已损坏的情况下。 此测试可确保该开机初期启动的已安装的 AM 驱动程序中存在相应的驱动程序的备份存储。
