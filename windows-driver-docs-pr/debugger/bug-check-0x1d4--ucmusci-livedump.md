---
title: Bug 检查 0x1D4 UCMUCSI_LIVEDUMP
description: UCMUCSI_LIVEDUMP 的实时转储的值为0x000001D4。
keywords:
- Bug 检查 0x1D4 UCMUCSI_LIVEDUMP
- UCMUCSI_LIVEDUMP
ms.date: 02/07/2020
topic_type:
- apiref
api_name:
- UCMUCSI_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 68ffee3e356c8b6b1c716d3c6f0bc2a4db5861db
ms.sourcegitcommit: cf8f0b13f33dfe97a94c8587f1f6797db24d1746
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075643"
---
# <a name="bug-check-0x1d4-ucmucsi_livedump"></a>Bug 检查0x1D4： UCMUCSI\_LIVEDUMP  

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

UCMUCSI_LIVEDUMP 的实时转储的值为0x000001D4。 这表示 UcmUcsi 类扩展遇到错误。 例如，这可能是因为 UCSI 命令超时，或因为客户端驱动程序返回失败而导致 UCSI 命令执行失败。

UcmUcsiCx 是包含的 UCSI 类扩展。 有关详细信息，请参阅[USB 类型 C 连接器系统软件接口（UCSI）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/ucsi)。

## <a name="ucmucsi_livedump-parameters"></a>UCMUCSI\_LIVEDUMP 参数

参数 | 说明
|---------|--------------|
1 | 失败类型-请参阅下面的值
2 | UCSI 命令值。
3 | 如果非零，则为指向附加信息的指针。 使用 `dt UcmUcsiCx!UCMUCSICX_TRIAGE` 显示。
4 | 保留。

**失败类型**

0x0： UCSI 命令超时，因为固件未及时响应命令。

0x1： UCSI 命令执行失败，原因可能是客户端驱动程序返回了故障或固件返回了错误代码。

## <a name="see-also"></a>另请参阅

[USB 团队博客-调试 UCSI 固件故障](https://techcommunity.microsoft.com/t5/microsoft-usb-blog/debugging-ucsi-firmware-failures/ba-p/283226)

[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)
