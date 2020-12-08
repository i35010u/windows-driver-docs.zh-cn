---
title: 签名类别和驱动程序安装
description: 签名类别和驱动程序安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29fa0c39d69bd8020029d32fb51e836c563a73aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838891"
---
# <a name="signature-categories-and-driver-installation"></a>签名类别和驱动程序安装


在 Windows Vista 和更高版本的 Windows 上安装驱动程序之前，操作系统会分析驱动程序的签名。 如果存在签名，Windows 会根据该签名验证所有驱动程序的文件。 根据此分析的结果，Windows 将驱动程序放入以下类别之一：

<a href="" id="signed-by-a-microsoft-windows-signing-authority--"></a>**由 Microsoft Windows 签名机构签名。**   
这些驱动程序可以是收件箱、由 WHQL 签名，也可以由 Windows 持续工程进行签名。

<a href="" id="signed-by-a-trusted-publisher--"></a>**由受信任的发布者签名。**   
这些驱动程序已由第三方签署，用户已明确选择始终信任此发布者提供的签名驱动程序。

<a href="" id="signed-by-an-untrusted-publisher--"></a>**由不受信任的发布者签名。**   
这些驱动程序已由第三方签署，用户已明确选择从不信任此发布者提供的驱动程序。

<a href="" id="signed-by-publisher-of-unknown-trust--"></a>**由未知信任的发布者签名。**   
这些驱动程序已由第三方进行签名，并且用户未指出是否信任此发布者。

<a href="" id="altered--"></a>**改动.**   
这些驱动程序已签名，但 Windows 检测到自签名包以来， [驱动程序包](driver-packages.md) 中至少一个文件发生了更改。

<a href="" id="unsigned--"></a>**无符号.**   
这些驱动程序未签名或签名无效。 必须使用受信任的证书颁发机构颁发的证书创建有效签名 (CA) 。

对该驱动程序进行分类后，Windows 将确定是否应该安装该驱动程序。 此过程取决于用户的类型。 对于非管理员和标准用户，Windows 不会提示用户。 它自动安装通过 Windows 签名颁发机构或受信任的发布者签名的驱动程序，并以无提示方式拒绝安装其他。

管理用户具有更大的灵活性：

-   如果驱动程序由 Windows 签名颁发机构或受信任的发布者进行签名，则 Windows 将安装驱动程序，而不提示用户。

-   如果驱动程序由不受信任的发布者签名，则 Windows 不会安装该驱动程序。 在这种情况下，Windows 不会提示用户，但会将错误记录到 *setupapi.log* 中。

-   如果驱动程序由未知信任的发布者签名，则 Windows 将提示用户使用以下 Windows 安全对话框。

    ![具有未知信任的驱动程序的 "windows 安全性" 对话框的屏幕截图](images/install1.png)

    用户必须明确选择是否安装此驱动程序。 用户还可以将发布者添加到用户系统上受信任的发布者列表。 如果用户选择此选项，则在用户的系统上安装以后，此发布服务器中的所有驱动程序都将被视为受信任。 如果用户未选择此选项，则发布服务器将保留在 "未知信任" 类别中，如果管理用户尝试从此发布服务器安装其他驱动程序，则会继续接收此提示。

-   如果驱动程序缺少有效签名或已更改，Windows 将使用以下 Windows 安全对话框提示管理员。 同样，用户必须明确选择是否安装驱动程序。

    ![没有有效签名的驱动程序的 "windows 安全性" 对话框的屏幕截图](images/install2.png)

**注意**  在 Windows Vista 和更高版本的 Windows 上，为了使用户能够播放下一代高级内容（如 HD DVD 以及在 *高级访问内容系统 (AACS) 规范* 下授权的其他格式），系统上的所有内核模式组件都必须进行签名。 这意味着，如果管理用户选择安装未签名或已更改的驱动程序，系统将不允许系统播放高级内容。 有关如何在 Windows Vista 中保护媒体组件的详细信息，请参阅 [Windows vista 中的受保护媒体组件的代码签名](https://go.microsoft.com/fwlink/p/?linkid=74262)。

 

 

 





