---
title: CM_PROB_UNSIGNED_DRIVER
description: CM_PROB_UNSIGNED_DRIVER
ms.assetid: 91d37d25-ca0d-413f-9e6f-5a22a0406714
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85a895d80e88c10f175a080bf5c160fb0570896a
ms.sourcegitcommit: aa7083b10b34a29a348f4950ced21a8a67a44a0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558411"
---
# <a name="cm_prob_unsigned_driver"></a>CM_PROB_UNSIGNED_DRIVER

此函数保留供系统使用。

设备没有在64位版本的 Windows 上启动，因为它的驱动程序未进行数字签名。 有关如何对驱动程序进行签名的详细信息，请参阅[驱动程序签名](driver-signing.md)。

## <a name="error"></a>错误

52

### <a name="display-message"></a>显示消息

"Windows 无法验证此设备所需驱动程序的数字签名。 最近的硬件或软件更改可能已安装了一个未正确或已损坏的文件，或者可能是来自未知来源的恶意软件。 （代码52） "

### <a name="recommended-resolution"></a>建议的解决方法

该驱动程序不符合[内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。

对于最终用户，避免此错误的唯一方法是获取并安装设备的数字签名驱动程序。

对于驱动程序开发人员，你可以使用各种方法在64位版本的 Windows 上加载未签名的驱动程序。 有关详细信息，请参阅[在开发和测试过程中安装未签名的驱动程序](installing-an-unsigned-driver-during-development-and-test.md)。

## <a name="see-also"></a>另请参阅

[代码完整性诊断系统日志事件](https://docs.microsoft.com/windows-hardware/drivers/install/code-integrity-diagnostic-system-log-events)
