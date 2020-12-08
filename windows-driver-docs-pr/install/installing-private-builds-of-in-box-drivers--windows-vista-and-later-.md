---
title: 安装收件箱驱动程序的专用版本
description: 安装收件箱驱动程序的专用版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82ab4cb74227eb8daf45d7897907b457677b936c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840693"
---
# <a name="installing-private-builds-of-inbox-drivers"></a>安装收件箱驱动程序的专用版本


从 Windows Vista 开始，操作系统提供了一种可安装更新版本的 Microsoft 签名驱动程序的机制。 否则，Microsoft 签署的驱动程序比第三方签署的驱动程序具有更高的选择值或 *排名*。 这使得驱动程序开发人员难以安装收件箱驱动程序的专用生成。

本部分介绍如何生成和安装 Windows 默认安装中包含的驱动程序的专用生成。 此类驱动程序称为 "*收件箱*" 驱动程序。

**注意**   若要理解此材料，必须熟悉对驱动程序进行数字签名，以及 Windows 如何根据此签名和其他条件对驱动程序进行排名。 有关驱动程序的数字签名的详细信息，请参阅 [驱动程序签名](driver-signing.md)。

 

以下主题介绍如何覆盖驱动程序的默认排名编号，以便可以安装收件箱驱动程序的专用生成：

[安装收件箱驱动程序的专用版本概述](overview-of-installing-private-builds-of-in-box-drivers.md)

[创建收件箱驱动程序的专用生成](creating-a-private-build-of-an-in-box-driver.md)

[将 Windows 配置为对驱动程序签名进行平等的分级](configuring-windows-to-rank-driver-signatures-equally.md)

[安装驱动程序包的已更新版本](installing-the-updated-version-of-the-driver-package.md)

**重要提示**   Windows 更新依赖于 Microsoft 签名的驱动程序，其优先级高于具有第三方签名的驱动程序。 将系统配置为覆盖此优先级可能会干扰 Windows 更新向使用者提供正确的驱动程序的能力。 对于 Windows 更新传递的驱动程序，这可能导致安装失败。

 

 

 





