---
title: 驱动程序签名策略
description: 驱动程序签名策略
keywords:
- 驱动程序签名 WDK，内核模式代码签名策略
- 对驱动程序进行签名 WDK，内核模式代码签名策略
- 数字签名 WDK，内核模式代码签名策略
- 签名 WDK，内核模式代码签名策略
- 内核模式代码签名策略 WDK
- 内核模式驱动程序签名 WDK
- 驱动程序包数字签名 WDK
- 包数字签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80c4bcc30169e18ee76d5ea6291a09fe21657a39
ms.sourcegitcommit: 18e027265862b9c6fe3acdb913299d68fc61c023
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2021
ms.locfileid: "99421897"
---
# <a name="driver-signing-policy"></a>驱动程序签名策略

> [!NOTE]
> 从 Windows 10 版本1607开始，Windows 将不会加载开发人员门户未签名的任何新的内核模式驱动程序。  若要对驱动程序进行签名，请首先 [注册 Windows 硬件开发人员中心计划](../dashboard/register-for-the-hardware-program.md)。 请注意，需要使用 [EV 代码签名证书](../dashboard/get-a-code-signing-certificate.md) 来建立仪表板帐户。

可以通过多种不同的方式将驱动程序提交到门户。  对于生产驱动程序，应按如下所述提交 HLK/HCK 测试日志。  对于仅限 Windows 10 客户端的系统进行测试，你可以提交用于 [证明签名](../dashboard/attestation-signing-a-kernel-driver-for-public-release.md)的驱动程序，这不需要进行 HLK 测试。  或者，你可以提交你的驱动程序以进行测试签名，如 [创建新的硬件提交](../dashboard/create-a-new-hardware-submission.md) 页中所述。

## <a name="exceptions"></a>例外

如果满足以下任一条件，则仍允许交叉签名的驱动程序：

* 计算机已从 Windows 的早期版本升级到版本1607。
* 安全启动在 BIOS 中处于关闭状态。
* 驱动程序已使用在2015年7月29日之前颁发的最终实体证书进行签名，该证书链接到受支持的交叉签名 CA。

为了防止系统无法正常启动，启动驱动程序将不会被阻止，但会被程序兼容性助手删除。

## <a name="signing-a-driver-for-client-versions-of-windows"></a>为 Windows 客户端版本的驱动程序签名

若要签署适用于 Windows 10 的驱动程序，请执行以下步骤：

1. 对于要在其上验证的每个版本的 Windows 10，下载适用于该版本的 Windows HLK (硬件实验室包) ，并针对该版本的客户端运行完整的证书传递。 每个版本都有一个日志。
2. 如果有多个日志，请使用最新的 HLK 将它们合并到单个日志中。
3. 将驱动程序和合并的 HLK 测试结果提交给 [Windows 硬件开发人员中心仪表板门户](../dashboard/index.yml)。

有关特定于版本的详细信息，请查看要作为目标的 Windows 版本的 [WHCP (Windows 硬件兼容性计划) 策略](/windows-hardware/design/compatibility/whcp-specifications-policies) 。

若要对 Windows 7、Windows 8 或 Windows 8.1 的驱动程序进行签名，请使用相应的 HCK (硬件认证工具包) 。  有关详细信息，请参阅 [Windows 硬件认证包用户指南](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))。

## <a name="signing-a-driver-for-earlier-versions-of-windows"></a>为 Windows 早期版本的驱动程序签名

在 Windows 10 1607 版之前，以下类型的驱动程序需要与 Microsoft 的交叉证书结合使用的验证码证书来进行交叉签名：

* 内核模式设备驱动程序
* 用户模式设备驱动程序
* 流式处理受保护内容的驱动程序。 这包括使用受保护的用户模式音频 (PUMA) 的音频驱动程序和用于处理受保护视频路径-输出保护管理的视频设备驱动程序)  (用于处理受保护视频路径-输出保护管理 (命令。 有关详细信息，请参阅 [受保护媒体组件的代码签名](https://download.microsoft.com/download/a/f/7/af7777e5-7dcd-4800-8a0a-b18336565f5b/pmp-sign.doc)。

## <a name="signing-requirements-by-version"></a>按版本的签名要求

下表显示了客户端操作系统版本的签名策略。

请注意，安全启动不适用于 Windows Vista 和 Windows 7。

|适用于：|Windows Vista、Windows 7;Windows 8 +，并关闭安全启动|Windows 8、Windows 8.1、Windows 10、版本1507、1511、安全启动|Windows 10 版本1607、1703、1709、安全启动|Windows 10，版本 1803 +，启用安全启动|
|--- |--- |--- |--- |--- |
|**架构**|仅限64位，无需32位的签名|64位，32位|64位，32位|64位，32位|
|**需要签名：**|嵌入文件或目录文件|嵌入文件或目录文件|嵌入文件或目录文件|嵌入文件或目录文件|
|**签名算法：**|SHA2|SHA2|SHA2|SHA2|
|**证书**|受代码完整性信任的标准根|受代码完整性信任的标准根|Microsoft 根证书颁发机构2010，microsoft 根证书颁发机构，Microsoft 根证书颁发机构|Microsoft 根证书颁发机构2010，microsoft 根证书颁发机构，Microsoft 根证书颁发机构|

除驱动程序代码签名外，还需要满足用于安装驱动程序的 PnP 设备安装签名要求。  有关详细信息，请参阅 [即插即用 (PnP) 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。

有关对 ELAM 驱动程序进行签名的信息，请参阅 [提前启动反恶意软件](/windows/desktop/w8cookbook/secured-boot)。

## <a name="signing-a-driver-for-internal-distribution-only"></a>仅针对内部分发对驱动程序进行签名

在某些情况下，可能需要在内部（而不是通过 Windows 更新）在内部分发驱动程序。  若要执行此操作而无需运行它的计算机处于测试模式，请使用以下过程：

1. [注册硬件开发人员中心](../dashboard/register-for-the-hardware-program.md)。
2. 查看 [硬件仪表板 FAQ](../dashboard/hardware-dashboard-faq.md) 并签署相应协议。
3. 上传 codesign 证书。
4. 使用已在合作伙伴中心注册的任何 codesign 证书以本地方式为驱动程序签名。
5. 包中的驱动程序，并使用上面的 codesign 证书对 CAB 进行签名。
6. 将 CAB 提交给硬件开发人员中心进行签名。
7. 如果提交已获批准，则硬件开发人员中心将使用 Microsoft 签名返回驱动程序。
8. 内部分发驱动程序。

## <a name="see-also"></a>另请参阅

* [在开发和测试过程中安装未签名的驱动程序包](installing-an-unsigned-driver-during-development-and-test.md)
* [为驱动程序签名以便公开发布](signing-drivers-for-public-release--windows-vista-and-later-.md)
* [在开发和测试期间签署驱动程序](./introduction-to-test-signing.md)
* [数字签名](driver-signing.md)
* [排查已签名驱动程序包的安装和加载问题](./detecting-driver-load-errors.md)
