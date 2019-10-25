---
title: 设置复制保护硬件
description: 设置复制保护硬件
ms.assetid: c9733d74-faa8-44af-8de7-9530ebcfe949
keywords:
- 复制保护 WDK 视频微型端口，设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e643811e5a227b40cbfa34435db34faa8603e3d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829504"
---
# <a name="setting-copy-protection-hardware"></a>设置复制保护硬件


## <span id="ddk_setting_copy_protection_hardware_gg"></span><span id="DDK_SETTING_COPY_PROTECTION_HARDWARE_GG"></span>


返回 VP\_标志的微型端口驱动程序\_在 VP\_命令的[**VIDEOPARAMETERS**](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)的**DWFLAGS**成员中受保护\_GET 应执行以下操作，以响应 VP\_命令\_SET 命令，具体取决于 VIDEOPARAMETERS 结构的**dwCPCommand**成员：

-   如果**dwCPCommand 是**的 VP\_CP\_CMD\_ACTIVATE，微型端口驱动程序应打开复制保护，并生成并返回**dwCPKey**中的唯一复制保护密钥。

-   如果**dwCPCommand 是**的 VP\_CP\_CMD\_停用，并且**dwCPKey**中的复制保护密钥有效，则微型端口驱动程序应关闭复制保护。

-   如果**dwCPCommand 是**的副总裁\_CP\_CMD\_更改并且**dwCPKey**中的复制保护密钥有效，则微型端口驱动程序应基于**bCP\_APSTriggerBits 中的触发器数据根据中的数据更改复制保护。** .

不具有复制保护硬件的设备的微型端口驱动程序只应在[**VRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)的**StatusBlock**的 "**状态**" 字段中返回 "无\_错误"。

 

 





