---
title: CM_PROB_UNSIGNED_DRIVER
description: CM_PROB_UNSIGNED_DRIVER
ms.assetid: 91d37d25-ca0d-413f-9e6f-5a22a0406714
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0fbaa9c4f60ac3b90072c21b24746d8c5287154
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327139"
---
# <a name="cmprobunsigneddriver"></a>CM_PROB_UNSIGNED_DRIVER

此函数保留供系统使用。

设备未在 64 位版本的 Windows 上启动，因为它具有未进行数字签名的驱动程序。 有关如何进行签名的驱动程序的详细信息，请参阅[驱动程序签名](driver-signing.md)。

## <a name="error"></a>错误

52

### <a name="display-message"></a>显示消息

"Windows 无法验证所需的此设备的驱动程序的数字签名。 最新的硬件或软件更改可能已安装的文件的签名不正确或损坏，或可能是从未知源的恶意软件。 （代码 52）"

### <a name="recommended-resolution"></a>建议的解决方法

该驱动程序不符合[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。

对于最终用户，避免此错误的唯一方法是获取和安装的设备进行数字签名的驱动程序。

为驱动程序开发人员可以使用各种方法来加载未签名的驱动程序在 64 位版本的 Windows。 有关详细信息，请参阅[开发和测试期间安装未签名的驱动程序](installing-an-unsigned-driver-during-development-and-test.md)。
