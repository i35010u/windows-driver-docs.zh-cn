---
title: 驱动程序签名策略
description: 驱动程序签名策略
ms.assetid: c3ba672c-5bf2-4885-a85e-fa6d8a47ca54
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
ms.openlocfilehash: 8aa60068e0cca799467ad4fa2148dc44c3a98cd0
ms.sourcegitcommit: f6aebb32c045b9da7da4bf9b3fd8d6fad05e9deb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/10/2020
ms.locfileid: "77114632"
---
# <a name="driver-signing-policy"></a>驱动程序签名策略

> [!NOTE]
> 从 Windows 10 版本1607开始，Windows 将不会加载开发人员门户未签名的任何新的内核模式驱动程序。  若要对驱动程序进行签名，请首先[注册 Windows 硬件开发人员中心计划](https://docs.microsoft.com/windows-hardware/drivers/dashboard/register-for-the-hardware-program)。 请注意，需要使用[EV 代码签名证书](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate)来建立仪表板帐户。

可以通过多种不同的方式将驱动程序提交到门户。  对于生产驱动程序，应按如下所述提交 HLK/HCK 测试日志。  对于仅限 Windows 10 客户端的系统进行测试，你可以提交用于[证明签名](../dashboard/attestation-signing-a-kernel-driver-for-public-release.md)的驱动程序，这不需要进行 HLK 测试。  或者，你可以提交你的驱动程序以进行测试签名，如[创建新的硬件提交](../dashboard/create-a-new-hardware-submission.md)页中所述。

## <a name="exceptions"></a>异常

如果满足以下任一条件，则仍允许交叉签名的驱动程序：

* 计算机已从 Windows 的早期版本升级到版本1607。
* 安全启动在 BIOS 中处于关闭状态。
* 驱动程序已使用在2015年7月29日之前颁发的最终实体证书进行签名，该证书链接到受支持的交叉签名 CA。

为了防止系统无法正常启动，启动驱动程序将不会被阻止，但会被程序兼容性助手删除。

## <a name="signing-a-driver-for-client-versions-of-windows"></a>为 Windows 客户端版本的驱动程序签名

若要签署适用于 Windows 10 的驱动程序，请执行以下步骤：

1. 对于想要在其上验证的每个版本的 Windows 10，下载适用于该版本的 Windows HLK （硬件实验室工具包），并对该版本的客户端运行完整的证书传递。 每个版本都有一个日志。
2. 如果有多个日志，请使用最新的 HLK 将它们合并到单个日志中。
3. 将驱动程序和合并的 HLK 测试结果提交给[Windows 硬件开发人员中心仪表板门户](../dashboard/index.yml)。

有关特定于版本的详细信息，请查看要作为目标的 Windows 版本的[WHCP （Windows 硬件兼容性计划）策略](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-specifications-policies)。

若要对 Windows 7、Windows 8 或 Windows 8.1 的驱动程序进行签名，请使用相应的 HCK （硬件认证工具包）。  有关详细信息，请参阅[Windows 硬件认证包用户指南](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))。

## <a name="signing-a-driver-for-earlier-versions-of-windows"></a>为 Windows 早期版本的驱动程序签名

在 Windows 10 1607 版之前，以下类型的驱动程序需要与 Microsoft 的交叉证书结合使用的验证码证书来进行交叉签名：

* 内核模式设备驱动程序
* 用户模式设备驱动程序
* 流式处理受保护内容的驱动程序。 这包括使用受保护用户模式音频（PUMA）的音频驱动程序和受保护的音频路径（PAP）以及处理受保护视频路径-输出保护管理（PVP-OPM）命令的视频设备驱动程序。 有关详细信息，请参阅[受保护媒体组件的代码签名](https://go.microsoft.com/fwlink/p/?linkid=74262)。

## <a name="signing-requirements-by-version"></a>按版本的签名要求

下表显示了客户端操作系统版本的签名策略。

请注意，安全启动不适用于 Windows Vista 和 Windows 7。

|适用范围：|Windows Vista、Windows 7;Windows 8 +，并关闭安全启动|Windows 8、Windows 8.1、Windows 10、版本1507、1511、安全启动|Windows 10 版本1607、1703、1709、安全启动|Windows 10，版本 1803 +，启用安全启动|
|--- |--- |--- |--- |--- |
|**架构**|仅限64位，无需32位的签名|64位，32位|64位，32位|64位，32位|
|**需要签名：**|嵌入文件或目录文件|嵌入文件或目录文件|嵌入文件或目录文件|嵌入文件或目录文件|
|**签名算法：**|SHA2|SHA2|SHA2|SHA2|
|**证书**|受代码完整性信任的标准根|受代码完整性信任的标准根|Microsoft 根证书颁发机构2010，microsoft 根证书颁发机构，Microsoft 根证书颁发机构|Microsoft 根证书颁发机构2010，microsoft 根证书颁发机构，Microsoft 根证书颁发机构|

除驱动程序代码签名外，还需要满足用于安装驱动程序的 PnP 设备安装签名要求。  有关详细信息，请参阅[即插即用（PnP）设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。

有关对 ELAM 驱动程序进行签名的信息，请参阅[提前启动反恶意软件](https://docs.microsoft.com/windows/desktop/w8cookbook/secured-boot)。

## <a name="see-also"></a>另请参阅

* [在开发和测试过程中安装未签名的驱动程序包](installing-an-unsigned-driver-during-development-and-test.md)
* [公开发布的签名驱动程序](signing-drivers-for-public-release--windows-vista-and-later-.md)
* [开发和测试期间对驱动程序进行签名](signing-drivers-during-development-and-test.md)
* [数字签名](driver-signing.md)
* [排查签名驱动程序包的安装和加载问题](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)
