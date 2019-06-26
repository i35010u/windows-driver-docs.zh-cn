---
title: Bug 检查 0x1D4 UCMUCSI_LIVEDUMP
description: UCMUCSI_LIVEDUMP 实时转储具有 0x000001D4 值。
keywords:
- Bug 检查 0x1D4 UCMUCSI_LIVEDUMP
- UCMUCSI_LIVEDUMP
ms.date: 02/22/2019
topic_type:
- apiref
api_name:
- UCMUCSI_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a20fb9166068558322d622b99f65e3c8acf9b3f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367569"
---
# <a name="bug-check-bug-check-0x1d4-ucmucsilivedump"></a>Bug 检查 Bug 检查 0x1D4:UCMUCSI\_LIVEDUMP  

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


UCMUCSI_LIVEDUMP 实时转储具有 0x000001D4 值。 

UcmUcsi.sys 驱动程序遇到错误。 UcmUcsi.sys 是一个框中 USB 连接器管理器 UCSI 客户端驱动程序。 有关详细信息，请参阅[USB 类型 C 连接器系统软件接口 (UCSI) 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/ucsi)。


## <a name="ucmucsilivedump-parameters"></a>UCMUCSI\_LIVEDUMP 参数

参数 | 描述 
|---------|--------------|
1 | 键入的失败-请参阅下面的值
2 | UCSI 命令值。
3 | 如果非零的附加信息的指针 (dt UcmUcsiCx ！UCMUCSICX_TRIAGE)。
4 | 保留。
 
**失败的类型**

0x0:UCSI 命令已超时，因为固件没有响应的命令的时间。

0x1:UCSI 命令执行失败，因为客户端驱动程序返回了失败或固件返回了错误代码。




