---
title: 设备管理器详细信息 "选项卡
description: 设备管理器详细信息 "选项卡
ms.assetid: 5f1e345f-72c6-4bd4-a0fa-304e5d0d91be
keywords:
- 设备管理器 WDK，详细信息选项卡
- 固件修订号 WDK 设备管理器
- 修订号 WDK 设备管理器
- 详细信息选项卡 WDK 设备管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5f92c8347abca45a050ec0cf7ae3e5c5958a65f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837509"
---
# <a name="device-manager-details-tab"></a>设备管理器详细信息 "选项卡

设备管理器提供每个设备的 "**详细信息**" 选项卡。 此选项卡显示许多对驱动程序开发人员和测试人员有用的信息，并帮助 Microsoft 客户支持服务（CSS）诊断客户问题。 该选项卡的页面显示[设备标识字符串](device-identification-strings.md)，以及在调试驱动程序时可能有用的设备和驱动程序配置信息。

## <a name="viewing-a-devices-details-tab"></a>查看设备的详细信息选项卡

默认情况下，"详细信息" 选项卡处于启用状态。 若要启用此选项卡，请将用户环境变量 DEVMGR_SHOW_DETAILS 设置为1。 设置此环境变量之后，设备的 "**详细信息**" 选项卡将在设备管理器中可用。 若要永久设置用户环境变量，请使用系统属性表的 "**高级**" 选项卡。

## <a name="providing-firmware-revision-numbers-for-the-details-tab"></a>为 "详细信息" 选项卡提供固件修订号

设备管理器的 "**详细信息**" 选项卡可以显示设备的固件修订号（如果可用）。 驱动程序可以通过响应 WMI 请求来提供固件修订号。 具体而言，驱动程序的[**DpWmiQueryDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)例程应通过返回 DEVICE_UI_FIRMWARE_REVISION 结构（在 Wmidata 中定义）来支持**MSDeviceUI_FirmwareRevision_GUID** 。 结构必须包含以 NULL 结尾的 WCHAR 字符串形式的固件修订号，其前面有一个包含字符串长度的 USHORT 值（包括**NULL**）。
