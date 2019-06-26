---
title: 设置复制保护硬件
description: 设置复制保护硬件
ms.assetid: c9733d74-faa8-44af-8de7-9530ebcfe949
keywords:
- 复制保护 WDK 微型端口设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d091be6c1e0db85d83196b8062c92d4951e27fb6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365578"
---
# <a name="setting-copy-protection-hardware"></a>设置复制保护硬件


## <span id="ddk_setting_copy_protection_hardware_gg"></span><span id="DDK_SETTING_COPY_PROTECTION_HARDWARE_GG"></span>


微型端口驱动程序返回副总裁\_标志\_中受保护[ **VIDEOPARAMETERS**](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)的**dwFlags**成员上副总裁\_命令\_GET 应执行以下操作以响应副总裁\_命令\_SET 命令，具体取决于**dwCPCommand** VIDEOPARAMETERS 结构中的成员：

-   如果**dwCPCommand**是副总裁\_CP\_CMD\_激活，微型端口驱动程序应打开复制保护和生成，并返回中的唯一复制保护键**dwCPKey**.

-   如果**dwCPCommand**是副总裁\_CP\_CMD\_停用和复制保护密钥**dwCPKey**有效，微型端口驱动程序应关闭复制保护。

-   如果**dwCPCommand**是副总裁\_CP\_CMD\_更改和复制保护密钥**dwCPKey**有效，微型端口驱动程序应更改复制保护基于中的数据中的触发器数据基于**bCP\_APSTriggerBits**。

不提供复制保护硬件的设备的微型端口驱动程序不应只需返回任何\_中的错误**状态**字段[ **VRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet)的**StatusBlock**。

 

 





