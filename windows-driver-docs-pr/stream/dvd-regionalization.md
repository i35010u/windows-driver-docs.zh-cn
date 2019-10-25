---
title: DVD 区域化
description: DVD 区域化
ms.assetid: 931441c8-9521-43c9-86f1-dbf75d36e190
keywords:
- DVD 解码器微型驱动程序 WDK
- 实行 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f6b456e2f27c01ef9a62bf9b6c93a712106104a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843214"
---
# <a name="dvd-regionalization"></a>DVD 区域化





DVD 解码器微型驱动程序不应涉及实行过程的任何部分。 流式处理体系结构的其他部分强制执行实行。 在大多数情况下，解码器微型驱动程序未实现[**KS\_DVDCOPY\_REGION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_region)属性。

如果解码器仅限于特定区域（通过硬件或其他注意事项），则它可能会响应**KS\_DVDCOPY\_region**属性以覆盖所有其他系统区域。 DVD 解码器微型驱动程序应正好设置一位，对应于为解码器指定的区域。 请注意，逻辑从媒体上的区域编码中*反转*。 例如，旨在仅在区域1（USA）中使用的解码器将0x01 返回到**KS\_DVDCOPY\_Region**属性。

如果解码器提供了区域，则系统区域更改应用程序仍将起作用。 如果系统中存在其他解码器，则会更改系统区域。 请注意，Windows DVD 播放仅在系统区域和解码器区域匹配时才起作用。

 

 




