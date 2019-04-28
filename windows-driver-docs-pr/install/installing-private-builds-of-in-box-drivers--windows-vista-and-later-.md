---
title: 安装收件箱驱动程序的专用版本
description: 安装收件箱驱动程序的专用版本
ms.assetid: 89170dff-284d-4d82-953c-46792158fbe5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91a860de23de38a93ea415f076d99fa49c1bcb66
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341484"
---
# <a name="installing-private-builds-of-inbox-drivers"></a>安装收件箱驱动程序的专用版本


从 Windows Vista 开始，操作系统提供了一种机制，可以安装更新版本的 Microsoft 签名的驱动程序。 否则，Microsoft 签名的驱动程序具有更高版本的选择值，或*排名*，比由第三方签名的驱动程序。 这使驱动程序开发人员若要安装的收件箱驱动程序的专用生成难。

本部分介绍如何生成和安装 Windows 的默认安装中包含的驱动程序对专用生成。 此类驱动程序被称为"*收件箱*"驱动程序。

**请注意**  若要了解此材料，你必须熟悉进行数字签名的驱动程序和 Windows 对基于该签名和其他条件的驱动程序的评级。 有关数字签名的驱动程序的详细信息，请参阅[驱动程序签名](driver-signing.md)。

 

下面的主题介绍如何为您的驱动程序覆盖默认等级数，以便可以安装专用生成的收件箱驱动程序：

[概述安装专用生成的收件箱驱动程序](overview-of-installing-private-builds-of-in-box-drivers.md)

[创建收件箱驱动程序对专用生成](creating-a-private-build-of-an-in-box-driver.md)

[配置 Windows 同样对驱动程序签名](configuring-windows-to-rank-driver-signatures-equally.md)

[安装驱动程序包的更新的版本](installing-the-updated-version-of-the-driver-package.md)

**重要**   Windows 更新依赖于 Microsoft 签名的驱动程序通过第三方的签名的驱动程序具有优先级。 配置重写此优先级的系统可能会影响 Windows 更新能够向用户提供正确的驱动程序。 这可能导致由 Windows Update 提供的驱动程序的安装失败。

 

 

 





