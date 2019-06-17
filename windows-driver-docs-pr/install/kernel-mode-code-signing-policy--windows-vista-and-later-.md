---
title: 驱动程序签名策略
description: 驱动程序签名策略
ms.assetid: c3ba672c-5bf2-4885-a85e-fa6d8a47ca54
keywords:
- 驱动程序签名 WDK，内核模式代码签名策略
- 签署驱动程序 WDK，内核模式代码签名策略
- 数字签名 WDK，内核模式代码签名策略
- 签名 WDK，内核模式代码签名策略
- 内核模式代码签署策略 WDK
- 内核模式驱动程序签名 WDK
- 驱动程序数据包数字签名 WDK
- 数据包数字签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f10b2686d411a2162b397f9392b47da67db5cbca
ms.sourcegitcommit: 91b989fc3256267fab89c36b1fa54ff039dcc687
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148530"
---
# <a name="driver-signing-policy"></a>驱动程序签名策略

> [!NOTE]
> 从 Windows 10，版本 1607 中，开始 Windows 不会加载未签名的开发人员门户的任何新内核模式驱动程序。  若要获取您的驱动程序签名，第一次[注册 Windows 硬件开发人员中心计划](https://docs.microsoft.com/windows-hardware/drivers/dashboard/register-for-the-hardware-program)。 请注意， [EV 代码签名证书](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate)建立仪表板帐户所需。

有许多不同的方法来提交到门户的驱动程序。  对于生产驱动程序，应如下所述提交 HLK/HCK 测试日志。  用于测试 Windows 10 客户端仅系统上，可提交驱动程序，以便[证明签名](../dashboard/attestation-signing-a-kernel-driver-for-public-release.md)，从而无需 HLK 测试。  或者，你可以将驱动程序进行测试签名提交上所述[创建新的硬件提交](../dashboard/create-a-new-hardware-submission.md)页。

## <a name="exceptions"></a>Exceptions

如果下列任何条件成立，仍允许跨签名的驱动程序：

* 在 PC 已从早期版本的 Windows 升级到 Windows 10，版本 1607年。
* 安全启动是关闭在 BIOS 中。
* 使用最终实体证书链接到受支持的交叉签名 CA 的 2015 年 7 月 29 之前颁发已签名的驱动程序。

若要防止系统无法正确启动，启动驱动程序将不会被阻止，但将通过程序兼容性助手将它们删除。

## <a name="signing-a-driver-for-client-versions-of-windows"></a>签名的 Windows 客户端版本的驱动程序

若要登录适用于 Windows 10 驱动程序，请执行以下步骤：

1. 有关你想要认证的 Windows 10 的每个版本，下载该版本的 Windows HLK （硬件实验室套件） 并针对该版本的客户端运行完整证书传递。 你将获得每个版本的一个日志。
2. 如果有多个日志，请将它们合并到单个日志使用最新的 HLK。
3. 提交您的驱动程序和合并的 HLK 测试结果[Windows 硬件开发人员中心仪表板门户](../dashboard/index.md)。

有关特定于版本的详细信息，请查看[WHCP （Windows 硬件兼容性计划） 策略](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-specifications-policies)想要面向的 Windows 版本。

若要注册 Windows 7、 8 或 Windows 8.1 驱动程序，使用适当的 HCK （硬件认证工具包）。  有关详细信息，请参阅[Windows 硬件认证工具包用户指南](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))。

## <a name="signing-a-driver-for-earlier-versions-of-windows"></a>签名的 Windows 早期版本的驱动程序

在 Windows 10，版本 1607 之前, 以下类型的驱动程序需要与 Microsoft 的交叉证书一起用于跨签名的验证码证书：

* 内核模式设备驱动程序
* 用户模式设备驱动程序
* 流式传输受保护的内容的驱动程序。 这包括使用受保护的用户模式音频 (PUMA) 和受保护的音频路径 (PAP)、 的音频驱动程序和视频的设备驱动程序处理受保护的视频路径输出保护管理 (PVP OPM) 命令。 有关详细信息，请参阅[代码签名的受保护的媒体组件](https://go.microsoft.com/fwlink/p/?linkid=74262)。

## <a name="signing-requirements-by-version"></a>按版本签名要求

下表显示了签名策略的客户端操作系统版本。

请注意，安全引导不适用于 Windows Vista 和 Windows 7。

|适用于：|Windows Vista，Windows 7;关闭 Windows 8 + 与安全启动|Windows 8 上的 Windows 8.1，Windows 10 版本 1507年和 1511 与安全启动|Windows 10，版本 1607年 + 与安全启动上|
|--- |--- |--- |--- |
|**体系结构：**|仅限 64 位、 所需的 32 位未签名|64 位、 32 位|64 位、 32 位|
|**所需的签名：**|嵌入或编录文件|嵌入或编录文件|嵌入或编录文件|
|**签名算法：**|SHA1|SHA1|SHA2 或 SHA1|
|**证书：**|标准根信任的代码完整性|标准根信任的代码完整性|Microsoft 的根颁发机构 2010，Microsoft 根证书颁发机构，Microsoft 根证书颁发机构|

除了签名的驱动程序代码，还需要符合即插即用设备安装签名安装驱动程序的要求。  有关详细信息，请参阅[插即用 (PnP) 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。

有关对 ELAM 驱动程序进行签名的信息，请参阅[早期启动反恶意软件](https://msdn.microsoft.com/library/windows/desktop/hh848061(v=vs.85).aspx)。

## <a name="see-also"></a>请参阅

* [在开发和测试期间安装未签名的驱动程序包](installing-an-unsigned-driver-during-development-and-test.md)
* [公开发布的版本的签名的驱动程序](signing-drivers-for-public-release--windows-vista-and-later-.md)
* [在开发和测试签名驱动程序](signing-drivers-during-development-and-test.md)
* [数字签名](driver-signing.md)
* [安装和已签名的驱动程序包的负载问题疑难解答](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)
