---
title: 使用更新的核心驱动程序构造包感知驱动程序
description: 使用更新的核心驱动程序构造包感知驱动程序
ms.assetid: 801ac83c-a04a-4a3f-81a9-24010a390ee5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e998d1c7793f524b846f5b3318765023fedcdb45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383161"
---
# <a name="constructing-a-package-aware-driver-with-updated-core-drivers"></a>使用更新的核心驱动程序构造包感知驱动程序


识别包的驱动程序可确保所有的包中的驱动程序组件进行配置用于点--打印操作过程。 指向并打印，Windows 用户而无需提供磁盘或其他安装媒体创建到远程打印机的连接。 相反，打印服务器会自动将打印驱动程序包下载到客户端。 有关详细信息，请参阅[指向并打印与驱动程序包](point-and-print-with-driver-packages.md)。

### <a name="including-updated-core-drivers"></a>包括更新的核心驱动程序

初始的 Windows Vista 版本包括只有一个核心驱动程序包。 该软件包包含 Ntprint.inf XPSDrv、 UniDrv 和 PostScript 核心驱动程序组件。 核心驱动程序包将定期更新，并可在主要 Windows 版本、 service pack 和分发的 Windows 可持续工程 (SE) 快速修复工程 (QFE) 包。 此包通常作为 Microsoft 独立更新 (MSU) 包，必须在安装 Windows MSU 安装程序 (Wusa.exe)-不是由即插即用安装程序分发。 从在即插即用安装中使用 MSU 提取核心驱动程序包的过程的说明，请参阅[获取更新核心驱动程序包](getting-the-updated-core-driver-package.md)。

此外，microsoft 将发布更新的核心驱动程序包[Connect](https://go.microsoft.com/fwlink/p/?linkid=133880) Web 站点主要 Windows 发行版和 service pack 后释放，并在这里，它们将可供任何人进行重新分发。 通常情况下，这些驱动程序的可用性滞后四到六周的主要 Windows 的更新。 使用这些驱动程序包的重新分发协议将可从 Microsoft Connect 网站获取的驱动程序包的过程。 如果 QFE 包可用于核心打印驱动程序，您可以直接从 Windows SE 获取 QFE 包并避免到 Microsoft Connect 网站的发布延迟。 你必须通过 Microsoft 技术客户经理 (TAM)，用户将要求您签署其他重新分发协议请求的 QFE 包。 从 Windows SE 的 QFE 包将与在 Microsoft Connect 网站上发布的相同。

如果您识别包的驱动程序包必须使用在初始 Windows Vista 版本中的版本比新的核心驱动程序包的版本，然后必须与识别包的驱动程序分发所需的核心驱动程序包。 请注意，Windows Vista 提供了任何机制来解决您的驱动程序的核心驱动程序依赖关系，如果所需的核心驱动程序包尚未在驱动程序存储区中。 此外，插即用 (PnP) 管理器不提供信息以帮助打印机安装程序，以确定所需的核心驱动程序包是在安装开始之前。 如果所需的核心驱动程序包不在驱动程序存储区中，安装将失败。 因此，如果一家制造商释放识别包的驱动程序需要的程序包，核心驱动程序包的更新的版本，版本必须包含所需的核心驱动程序包，以确保安装成功。

**请注意**  如果可能，避免使您识别包的驱动程序的包依赖于比初始 Windows Vista 版本的系统提供的核心驱动程序包。 否则，必须采取额外步骤以确保正确驱动程序包安装在 Windows Vista 版本和较旧版本的核心驱动程序包。

 

本地化的帮助内容包含在核心驱动程序包，但初始 Windows Vista 推出后，将不会更新此内容。 驱动程序包的语言，在选择时使用最有可能可理解的这些安装包的语言。 通常情况下，想要的单个包，以涵盖多种语言提供的制造商应使用英语。 所选驱动程序包的语言不会影响客户端计算机上已提供的本地化的帮助内容。

MSU 文件是特定于处理器体系结构 (x86 和 x64 IA64)。 请务必选择适当的体系结构为您的驱动程序。 作为一个选项，你可以提供捆绑在一起的两个或多个体系结构使用通用 INF 文件的二进制驱动程序文件的多体系结构驱动程序包。 如果提供多体系结构驱动程序包，您的版本应包括支持的每个体系结构的单独的核心驱动程序包。

本部分讨论以下主题：

[获取更新的核心驱动程序包](getting-the-updated-core-driver-package.md)

[捆绑包识别驱动程序使用的核心驱动程序](bundling-the-core-driver-with-your-package-aware-driver.md)

[更新包识别驱动程序的 INF](updating-your-package-aware-driver-s-inf.md)

 

 




