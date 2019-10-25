---
title: NFP 设备标识符
description: NFP 设备标识符
ms.assetid: B387D3F8-A9A7-47F0-B5E3-8437581947E4
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41543e6ac407fb9fc607729272b4d605582422da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843425"
---
# <a name="nfp-device-identifiers"></a>NFP 设备标识符


以下是 NFP 设备驱动程序的设备标识符：

-   设备接口类
    -   DEVINTERFACE\_NFP 的 GUID\_
    -   "{FB3842CD-9E2A-4F83-8FCC-4B0761139AE9}"
-   设备类 GUID
    -   "{5630831C-06C9-4856-B327-F5D32586E060}"
-   设备类
    -   程度
    -   这是从 Windows 8 开始的操作系统定义的设备类。 公开此接口的驱动程序必须与此设备类相匹配。
-   DEVPKEY\_NFP\_功能
    -   0xFB3842CD、0x9E2A、0x4F83、0x8F、0xCC、0x4B、0x07、0x61、0x13、0x9A、0xE9、0x02

如果设备被播发为 NFC，驱动程序必须在公开的 GUID\_DEVINTERFACE\_NFP 接口上填充 DEVPKEY\_NFP\_功能，其中包含 DEVPROP\_类型\_STRING\_LIST 属性条目： "StandardNfc"。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

