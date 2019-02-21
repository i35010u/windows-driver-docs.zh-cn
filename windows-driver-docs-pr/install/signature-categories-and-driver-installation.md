---
title: 签名类别和驱动程序安装
description: 签名类别和驱动程序安装
ms.assetid: d5b0e3a3-51c3-40d8-a2dc-c9392feff2cb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 553a0c6855a958259a303d471c9d8ff6a9457dee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546058"
---
# <a name="signature-categories-and-driver-installation"></a>签名类别和驱动程序安装


Windows Vista 和更高版本的 Windows 安装的驱动程序之前，操作系统将分析驱动程序签名。 如果存在签名，则 Windows 验证针对该签名的驱动程序的所有文件。 基于此分析的结果，Windows 将放入驱动程序中的以下类别之一：

<a href="" id="signed-by-a-microsoft-windows-signing-authority--"></a>**由 Microsoft Windows 签名颁发机构签名。**   
这些驱动程序是任一收件箱，由 WHQL 签名或签名的 Windows 可持续工程。

<a href="" id="signed-by-a-trusted-publisher--"></a>**由受信任的发行者签名。**   
这些驱动程序签名的第三方，且用户已显式选择，以便始终信任来自此发布者签名的驱动程序。

<a href="" id="signed-by-an-untrusted-publisher--"></a>**由不受信任的发布者签名。**   
这些驱动程序签名的第三方，并且用户已显式选择了永远不会信任来自此发布服务器的驱动程序。

<a href="" id="signed-by-publisher-of-unknown-trust--"></a>**由未知的信任的发布者签名。**   
这些驱动程序签名的第三方，并在用户尚未指示是否信任此发布服务器。

<a href="" id="altered--"></a>**更改。**   
这些驱动程序进行签名，但 Windows 检测到该至少一个文件中的[驱动程序包](driver-packages.md)已签名后已被更改。

<a href="" id="unsigned--"></a>**无符号。**   
这些驱动程序为无符号或具有无效签名。 使用由受信任证书颁发机构 (CA) 颁发的证书，必须创建有效的签名。

该驱动程序进行分类后，Windows 将确定是否应安装。 该过程取决于用户的类型。 对于非管理性和标准用户，Windows 不会提示用户。 它会自动安装驱动程序通过 Windows 签名颁发机构或受信任的发行者签名，并以无提示方式将拒绝所有其他安装。

管理用户拥有更大的灵活性：

-   如果驱动程序由 Windows 签名颁发机构或受信任的发行者签名，Windows 不提示用户安装该驱动程序。

-   如果该驱动程序已由不受信任的发行者签名，Windows 将不安装该驱动程序。 Windows 不会提示用户在这种情况下，但记录到错误*Setupapi.dev.log*。

-   如果驱动程序由未知的信任的发布者签名，Windows 会提示用户使用以下 Windows 安全对话框。

    ![驱动程序具有未知的信任关系的 windows 安全对话框的屏幕截图](images/install1.png)

    用户必须明确选择是否要安装此驱动程序。 该用户也是能够将发布服务器添加到用户的系统上的受信任发布者的列表。 如果用户选择此选项时，来自此发布服务器的所有将来的驱动程序将被视为受信任的用户的系统上安装时。 如果用户未选择此选项，该发布服务器将保持在未知的信任类别和管理用户将继续接收此提示，如果在尝试安装此发布服务器上的其他驱动程序。

-   如果该驱动程序缺少有效的签名，或者已被更改，Windows 将提示管理员提供以下的 Windows 安全对话框。 同样，用户必须明确选择是否要安装驱动程序。

    ![没有有效签名的驱动程序的 windows 安全对话框的屏幕截图](images/install2.png)

**请注意**  在 Windows Vista 和更高版本的 Windows，以便用户以用于播放下一代高级内容，如 HD DVD 和授予许可的其他格式*高级访问内容系统 (AACS)规范*，必须对其系统上的所有内核模式组件进行都签名。 这意味着，如果管理用户选择此选项可以安装未签名或更改的驱动程序，系统不允许播放的高级内容。 有关如何保护在 Windows Vista 中的媒体组件的详细信息，请参阅[代码签名的 Windows Vista 中受保护的媒体组件](https://go.microsoft.com/fwlink/p/?linkid=74262)。

 

 

 





