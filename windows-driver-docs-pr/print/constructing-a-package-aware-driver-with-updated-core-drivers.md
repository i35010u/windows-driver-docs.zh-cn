---
title: 使用更新的核心驱动程序构造包感知驱动程序
description: 使用更新的核心驱动程序构造包感知驱动程序
ms.assetid: 801ac83c-a04a-4a3f-81a9-24010a390ee5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c4872f60cacd95f1f7adaf254ecc1effc22bcba
ms.sourcegitcommit: f0e54ea159d168a77643bf2e098d6b90e92b528c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455561"
---
# <a name="constructing-a-package-aware-driver-with-updated-core-drivers"></a>使用更新的核心驱动程序构造包感知驱动程序

包感知驱动程序可确保包中的所有驱动程序组件都配置为在点和打印操作期间使用。 使用 "点和打印"，Windows 用户可以在不提供磁盘或其他安装媒体的情况下，创建到远程打印机的连接。 相反，打印服务器会自动将打印驱动程序包下载到客户端。 有关详细信息，请参阅[通过驱动程序包进行点和打印](point-and-print-with-driver-packages.md)。

## <a name="including-updated-core-drivers"></a>包括更新的核心驱动程序

最初的 Windows Vista 版本仅包含一个核心驱动程序包。 该包包含 Ntprint.inf 以及 XPSDrv、UniDrv 和 PostScript 核心驱动程序组件。 核心驱动程序包将定期更新，并在主要 Windows 版本、service pack 和 Windows 持续工程（SE）分发的快速修补工程（QFE）包中提供。 此包通常作为 Microsoft 独立更新（MSU）包分发，必须由 Windows MSU 安装程序（Wusa）安装，而不是由 PnP 安装程序安装。 有关从 MSU 提取核心驱动程序包以供在 PnP 安装中使用的过程的说明，请参阅[获取更新后的核心驱动程序包](getting-the-updated-core-driver-package.md)。

如果 QFE 包可用于核心打印驱动程序，则可以直接从 Windows SE 获取 QFE 包。 必须通过 Microsoft 技术客户经理（TAM）请求 QFE 包，该管理包将要求你签署额外的再发行协议。

如果你的包感知驱动程序包必须使用比初始 Windows Vista 版本中版本新的核心驱动程序包版本，则必须使用包感知驱动程序分发所需的核心驱动程序包。 请注意，如果驱动程序存储区中尚不存在所需的核心驱动程序包，则 Windows Vista 不提供解析驱动程序核心驱动程序依赖项的机制。 此外，即插即用（PnP）管理器不提供任何信息来帮助打印机安装程序确定在安装开始之前是否可以使用所需的核心驱动程序包。 如果所需核心驱动程序包不在驱动程序存储区中，则安装将失败。 因此，如果制造商发布了需要核心驱动程序包的更新版本的包感知驱动程序包，则版本必须包含所需的核心驱动程序包，以确保安装成功。

> [!NOTE]
> 如果可能，请避免使包感知驱动程序包依赖于系统提供的、比初始 Windows Vista 版本新的核心驱动程序包。 否则，你必须执行额外的步骤，以确保你的驱动程序包正确地安装在具有较旧版本核心驱动程序包的 Windows Vista 版本上。

核心驱动程序包中包含本地化的帮助内容，但在首次发布 Windows Vista 之后，此内容不会更新。 为驱动程序包选择语言时，请使用安装包的方法最可能理解的语言。 通常，想要装运单个包裹以涵盖多种语言的制造商应使用英语。 为驱动程序包选择某种语言不会影响客户端计算机上已有的已提供本地化的帮助内容。

MSU 文件特定于处理器体系结构（IA64、x86 和 x64）。 请确保为驱动程序选择适当的体系结构。 作为选项，你可以提供一个多体系结构驱动程序包，该程序包将两个或多个体系结构的二进制驱动程序文件捆绑到一个公用 INF 文件中。 如果提供多体系结构驱动程序包，则发布应为每个受支持的体系结构包含单独的核心驱动程序包。

本部分介绍以下主题：

[获取更新的核心驱动程序包](getting-the-updated-core-driver-package.md)

[将核心驱动程序与包感知驱动程序捆绑到一起](bundling-the-core-driver-with-your-package-aware-driver.md)

[更新包感知驱动程序的 INF](updating-your-package-aware-driver-s-inf.md)
