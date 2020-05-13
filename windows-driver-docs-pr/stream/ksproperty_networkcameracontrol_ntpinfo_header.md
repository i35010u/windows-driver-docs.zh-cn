---
title: KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_HEADER （ksmedia）
description: 包含用于在 Onvif 协议相机上设置或禁用 NTP 服务器的特定于 NTP 的负载。
ms.date: 04/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: ef53a88275d3b695c2eb8461afb4a0a38481220a
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270440"
---
# <a name="ksproperty_networkcameracontrol_ntpinfo_header-structure"></a>KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_HEADER 结构

**KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_HEADER**结构包含用于设置或禁用 Onvif 协议相机上的 ntp 服务器的特定于 ntp 的负载。

## <a name="syntax"></a>语法

```cpp
typedef struct
{
  ULONG Size;
  KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_TYPE Type;
} KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_HEADER, *PKSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_HEADER;
```

## <a name="members"></a>成员

### <a name="size"></a>大小

NTP 专用有效负载的大小。

### <a name="type"></a>类型

包含[KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_networkcameracontrol_ntpinfo_type)枚举中的值之一。

## <a name="remarks"></a>备注

此命令将用于在 Onvif 协议相机上设置或禁用 NTP 服务器。 应用程序可以选择将照相机配置为使用本地计算机使用的相同 NTP 服务器（例如，正在控制照相机的 Windows 设备）。它还可以用于将照相机配置为使用自定义 NTP 服务器。

通过分析 SYSTEM \\ CurrentControlSet \\ Services \\ W32Time \\ 参数处的注册表值找到本地 PC 的 NTP 服务器条目 \\ 。 应用可以扫描以空格分隔的注册表值，以便在照相机上设置最适合的服务器。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- | --- |
| Header | ksmedia （包括 Ksmedia） |

## <a name="see-also"></a>另请参阅

[KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_networkcameracontrol_ntpinfo_type)

[KSPROPERTY_NETWORKCAMERACONTROL_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_networkcameracontrol_property)
