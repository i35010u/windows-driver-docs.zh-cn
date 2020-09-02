---
title: NFP 设备标识符
description: NFP 设备标识符
ms.assetid: B387D3F8-A9A7-47F0-B5E3-8437581947E4
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6db5d49c2b202fb92c7364d9548d0d3f4354f038
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382831"
---
# <a name="nfp-device-identifiers"></a>NFP 设备标识符


以下是 NFP 设备驱动程序的设备标识符：

-   设备接口类
    -   GUID \_ DEVINTERFACE \_ NFP
    -   "{FB3842CD-9E2A-4F83-8FCC-4B0761139AE9}"
-   设备类 GUID
    -   "{5630831C-06C9-4856-B327-F5D32586E060}"
-   设备分类
    -   程度
    -   这是从 Windows 8 开始的操作系统定义的设备类。 公开此接口的驱动程序必须与此设备类相匹配。
-   DEVPKEY \_ NFP \_ 功能
    -   0xFB3842CD、0x9E2A、0x4F83、0x8F、0xCC、0x4B、0x07、0x61、0x13、0x9A、0xE9、0x02

如果设备被播发为 NFC，则驱动程序必须 \_ \_ 在公开的 GUID DEVINTERFACE NFP 接口上填充 DEVPKEY NFP 功能，其中 \_ \_ \_ \_ \_ 包含一个包含一个条目的 DEVPROP TYPE STRING LIST 属性： "StandardNfc"。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)