---
title: 设备管理器详细信息选项卡
description: 设备管理器详细信息选项卡
ms.assetid: 5f1e345f-72c6-4bd4-a0fa-304e5d0d91be
keywords:
- 设备管理器 WDK，详细信息选项卡
- 固件修订版号 WDK 设备管理器
- 修订号 WDK 设备管理器
- 详细信息选项卡上的 WDK 设备管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58a78d25c9337b6115c48481810560df69f3446f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521600"
---
# <a name="device-manager-details-tab"></a>设备管理器详细信息选项卡

设备管理器提供了**详细信息**为每个设备的选项卡。 此选项卡的驱动程序开发人员和测试人员，显示很多有用的信息，并有助于 Microsoft 客户支持服务 (CSS) 诊断客户问题。 选项卡的页面将显示[设备标识字符串](device-identification-strings.md)一起使用时调试驱动程序会很有用的设备和驱动程序配置信息。

## <a name="viewing-a-devices-details-tab"></a>查看设备的详细信息选项卡

默认情况下启用详细信息选项卡。 若要启用此选项卡，设置为 1 的用户环境变量 DEVMGR_SHOW_DETAILS。 设置此环境变量之后,**详细信息**设备的选项卡将为设备管理器中可用。 若要永久设置的用户环境变量，使用**高级**系统属性表选项卡。

## <a name="providing-firmware-revision-numbers-for-the-details-tab"></a>有关详细信息选项卡提供固件修订号

设备管理器**详细信息**选项卡可显示设备的固件修订号，如果可用。 驱动程序可以通过响应 WMI 请求提供固件修订号。 具体而言，驱动程序[ **DpWmiQueryDataBlock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)例程应支持**MSDeviceUI_FirmwareRevision_GUID**通过返回 DEVICE_UI_FIRMWARE_REVISION（在 Wmidata.h 中定义） 的结构。 该结构必须包含固件修订号为以 NULL 结尾的 WCHAR 字符串，前面有一个包含字符串长度的 USHORT 值 (包括**NULL**)。
