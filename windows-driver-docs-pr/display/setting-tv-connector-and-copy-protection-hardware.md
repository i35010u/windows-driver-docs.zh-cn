---
title: 设置电视连接器和复制保护硬件
description: 设置电视连接器和复制保护硬件
ms.assetid: 2de45c31-6a44-4a57-84b9-3cb21c905f4b
keywords:
- 电视连接器 WDK 视频微型端口
- 复制保护 WDK 视频微型端口，设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c8e31e9c88f68e5281b9164112566df1ab35414
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065994"
---
# <a name="setting-tv-connector-and-copy-protection-hardware"></a>设置电视连接器和复制保护硬件


## <span id="ddk_setting_tv_connector_and_copy_protection_hardware_gg"></span><span id="DDK_SETTING_TV_CONNECTOR_AND_COPY_PROTECTION_HARDWARE_GG"></span>


对于[**VIDEOPARAMETERS**](/windows/desktop/api/tvout/ns-tvout-_videoparameters)上的**dwFlags**成员中的微型端口驱动程序设置的任何位 \_ \_ ，小型端口驱动程序可以对 vp 命令集执行一组设置 \_ \_ 。 调用方负责调用微型端口驱动程序，以便仅设置微型端口驱动程序在 VP 命令获取上支持的功能 \_ \_ 。 小型端口驱动程序应通过将硬件设置为 \_ 每个 VIDEOPARAMETERS 字段的值来响应 VP 命令集，在 \_ **dwFlags**中设置相应的位。 例如：

-   如果微型端口驱动程序 \_ \_ \_ 在 vp 命令获取上设置副总裁标志电视模式位 \_ \_ ，则微型端口驱动程序应将电视模式更改为 **dwMode** 指定的值 \_ \_ \_ \_ \_ 。

-   如果微型端口驱动程序 \_ \_ \_ 在 vp 命令获取上设置副总裁标志电视标准位 \_ \_ ，则微型端口驱动程序应将电视标准更改为 **dwTVStandard** 指定的值 \_ \_ \_ \_ \_ 。

-   如果微型端口驱动程序 \_ \_ 在 vp 命令获取上设置副总裁标志对比度 \_ \_ ，则微型端口驱动程序应将对比度设置为 **dwContrast** 指定的值 \_ \_ \_ \_ 。

如果未在 **dwFlags**中设置相应的位，则 VIDEOPARAMETERS 字段包含未定义的数据。

 

