---
title: NFP 设备标识符
description: NFP 设备标识符
ms.assetid: B387D3F8-A9A7-47F0-B5E3-8437581947E4
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35c5832c12c7748297d1215d79f1fef8d7323dff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523659"
---
# <a name="nfp-device-identifiers"></a>NFP 设备标识符


以下是 NFP 设备驱动程序的设备标识符：

-   设备接口类
    -   GUID\_DEVINTERFACE\_NFP
    -   "{FB3842CD-9E2A-4F83-8FCC-4B0761139AE9}"
-   设备类 GUID
    -   “{5630831C-06C9-4856-B327-F5D32586E060}”
-   设备类
    -   "邻近"
    -   这是从 Windows 8 开始 OS 定义的设备类。 将此接口公开的驱动程序必须与此设备类匹配。
-   DEVPKEY\_NFP\_功能
    -   0xFB3842CD, 0x9E2A, 0x4F83, 0x8F, 0xCC, 0x4B, 0x07, 0x61, 0x13, 0x9A, 0xE9, 0x02

如果设备已公布为 NFC，驱动程序必须填充 DEVPKEY\_NFP\_上公开的 GUID 的功能\_DEVINTERFACE\_DEVPROP NFP 接口\_类型\_字符串\_列表属性包含一个条目："StandardNfc"。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

