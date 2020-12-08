---
title: CM_PROB_UNSIGNED_DRIVER
description: CM_PROB_UNSIGNED_DRIVER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81942ed1726b92b53589cb9eea4f124fcb12c77d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783063"
---
# <a name="code-52---cm_prob_unsigned_driver"></a>代码 52 - CM_PROB_UNSIGNED_DRIVER

此设备管理器错误消息表明设备没有在64位版本的 Windows 上启动，因为它的驱动程序未进行数字签名。 有关如何对驱动程序进行签名的详细信息，请参阅 [驱动程序签名](driver-signing.md)。

## <a name="error"></a>错误

52

### <a name="display-message"></a>显示消息

"Windows 无法验证此设备所需驱动程序的数字签名。 最近的硬件或软件更改可能已安装了一个未正确或已损坏的文件，或者可能是来自未知来源的恶意软件。  (代码 52) "

### <a name="recommended-resolution"></a>推荐的解决方案

该驱动程序不符合 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。

对于最终用户，避免此错误的唯一方法是获取并安装设备的数字签名驱动程序。

对于驱动程序开发人员，你可以使用各种方法在64位版本的 Windows 上加载未签名的驱动程序。 有关详细信息，请参阅 [在开发和测试过程中安装未签名的驱动程序](installing-an-unsigned-driver-during-development-and-test.md)。

## <a name="see-also"></a>另请参阅

[代码完整性诊断系统日志事件](./code-integrity-diagnostic-system-log-events.md)
