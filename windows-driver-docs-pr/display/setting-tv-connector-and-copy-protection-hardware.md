---
title: 设置电视连接器和复制保护硬件
description: 设置电视连接器和复制保护硬件
ms.assetid: 2de45c31-6a44-4a57-84b9-3cb21c905f4b
keywords:
- 电视连接器 WDK 微型端口
- 复制保护 WDK 微型端口设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e3c1258bb71c9df2234d4575cd2278a5cd980ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339701"
---
# <a name="setting-tv-connector-and-copy-protection-hardware"></a>设置电视连接器和复制保护硬件


## <span id="ddk_setting_tv_connector_and_copy_protection_hardware_gg"></span><span id="DDK_SETTING_TV_CONNECTOR_AND_COPY_PROTECTION_HARDWARE_GG"></span>


为任何通过中的微型端口驱动程序设置的位**dwFlags**的成员[ **VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff570173)上副总裁\_命令\_GET、 微型端口驱动程序可以执行一组副总裁\_命令\_设置。 调用要设置仅微型端口驱动程序为其指示副总裁上的支持该功能的微型端口驱动程序的调用方负责\_命令\_获取。 微型端口驱动程序应响应副总裁\_命令\_设置设置为其每个 VIDEOPARAMETERS 字段中设置了相应的位的值与硬件**dwFlags**。 例如：

-   如果微型端口驱动程序设置副总裁\_标志\_电视\_模式位副总裁\_命令\_获得，微型端口驱动程序应将电视模式更改为指定的值，然后**dwMode**时副总裁\_标志\_电视\_模式设置上副总裁\_命令\_设置。

-   如果微型端口驱动程序设置副总裁\_标志\_电视\_标准位副总裁\_命令\_获得，则微型端口驱动程序应更改电视标准指定的值为**dwTVStandard**时副总裁\_标志\_电视\_标准设置上副总裁\_命令\_设置。

-   如果微型端口驱动程序设置副总裁\_标志\_对比度位副总裁\_命令\_获取，则微型端口驱动程序应设置为指定的值的对比度**dwContrast**时副总裁\_标志\_对比度设置上副总裁\_命令\_设置。

VIDEOPARAMETERS 字段包含未定义的数据，如果未设置相应的位**dwFlags**。

 

 





