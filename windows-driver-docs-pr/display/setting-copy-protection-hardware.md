---
title: 设置复制保护硬件
description: 设置复制保护硬件
keywords:
- 复制保护 WDK 视频微型端口，设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7841ccc83029e74d5170a7890db9d67ed58cff3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816793"
---
# <a name="setting-copy-protection-hardware"></a>设置复制保护硬件


## <span id="ddk_setting_copy_protection_hardware_gg"></span><span id="DDK_SETTING_COPY_PROTECTION_HARDWARE_GG"></span>


在 \_ \_ vp 命令获取中，在 [**VIDEOPARAMETERS**](/windows/win32/api/tvout/ns-tvout-videoparameters)的 **dwFlags** 成员中保护的、返回的带 vp 标志的微型端口驱动程序 \_ \_ 应执行以下操作，以响应 VP \_ 命令 \_ 集命令，具体取决于 VIDEOPARAMETERS 结构的 **dwCPCommand** 成员：

-   如果 **dwCPCommand** 是将 \_ CP \_ CMD \_ ACTIVATE 激活，微型端口驱动程序应打开复制保护，并在 **dwCPKey** 中生成并返回唯一的复制保护密钥。

-   如果 **dwCPCommand** 是 \_ \_ \_ 在 **dwCPKey** 中启用的 "CP" CMD "停用" 和 "复制保护密钥"，则微型端口驱动程序应关闭复制保护。

-   如果 **dwCPCommand** 是 ""，则 " \_ CP \_ CMD \_ 更改" 和 " **dwCPKey** 中的复制保护密钥" 有效，微型端口驱动程序应基于 **bCP \_ APSTriggerBits** 中的触发器数据根据中的数据更改复制保护。

不具有复制保护硬件的设备的微型端口驱动程序只应 \_ 在 [**VRP**](/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)的 **StatusBlock** 的 "**状态**" 字段中返回 "无错误"。

 

