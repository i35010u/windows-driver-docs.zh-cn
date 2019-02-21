---
title: 使用自定义硬件 Id 和兼容 Id
description: 使用自定义硬件 Id 和兼容 Id
ms.assetid: 4f0ae082-b601-4322-add8-63941c2bdad3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c5e18696706d9e787f395829baa553a437b3e4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545800"
---
# <a name="using-custom-hardware-ids-and-compatible-ids"></a>使用自定义硬件 Id 和兼容 Id


如中所述[设备标识字符串](device-identification-strings.md)，以下是新的总线驱动程序应使用插即用 (PnP) 硬件 Id 和兼容 Id 的通用格式。

```cpp
enumerator\enumerator-specific-device-ID 
```

其中：

-   *枚举器*标识*枚举器*（总线驱动程序） 的检测并向即插即用的管理器的总线上报告子设备。

-   *枚举器特定于设备 ID*指定枚举器特定于设备标识符。

如果配置或操作的总线明显不同于其他总线，总线总线驱动程序应使用唯一的枚举器名称以确保，总线子设备不会无意中并不恰当地分组与子设备由总线驱动程序为枚举这些其他总线。 总线驱动程序应使用报表向 PnP 管理器的设备标识字符串的以下格式：

```cpp
bus-type-guid\vendor-specific-id
```

其中：

-   *总线类型 guid*是唯一的 GUID，用于标识在总线并应为相同的 GUID 用于标识在总线。 如中所述[安装总线驱动程序](installing-a-new-bus-driver.md)，总线驱动程序的标识响应中的设备的总线类型[ **IRP_MN_QUERY_BUS_INFORMATION** ](https://msdn.microsoft.com/library/windows/hardware/ff551654)对设备的请求。

-   *供应商特定 id*是供应商定义的格式通常标识供应商、 设备、 子系统、 修订号和可能是选择其他设备信息。 例如，格式可能需要的窗体*供应商*&*设备*&*子系统*&*修订版本，* 其中 & 号字符 ("&") 分隔子文件夹和每个子字段的格式是特定于供应商。 实际的设备标识字符串的示例，请参阅[设备标识字符串](device-identification-strings.md)。

PnP 管理器将发送[ **IRP_MN_QUERY_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551679)到总线驱动程序的请求以获取设备的设备标识字符串。 设备标识字符串包括设备 ID、 设备实例 ID、 硬件 Id 的列表和兼容 Id 列表。 以下虚构示例包括设备 ID、 硬件 Id 的列表和兼容 Id 列表。 在这些示例中，指定枚举器*总线类型 guid*子字段，即"{17ed6609-9bc8-44ca-8548-abb79b13781b}"的 GUID。 格式*供应商特定 id*字段是*供应商*&*设备*&*子系统*&*修订*，其中*供应商*子字段是"ven_1"*设备*子字段是"dev_2"*子系统*子字段是"subsys_3"，并*修订*子字段是"rev_4"。

设备 ID 是设备的最具体的说明的硬件 ID。 在以下示例中，设备 ID 指定供应商、 设备、 子系统和修订号。

```cpp
{17ed6609-9bc8-44ca-8548-abb79b13781b}\ven_1&dev_2&subsys_3&rev_4 
```

硬件 ID 列表指定 Id 的顺序，从最具体到最不具体。 在以下列表中，设备标识字符串将被报告为硬件 ID，如果供应商、 设备和子系统至少指定了。 首先列出包括的大多数信息的硬件 ID。

```cpp
{17ed6609-9bc8-44ca-8548-abb79b13781b}\ven_1&dev_2&subsys_3&rev_4 
{17ed6609-9bc8-44ca-8548-abb79b13781b}\ven_1&dev_2&subsys_3 
```

以下列表中，设备标识字符串被报告为兼容 ID 如果它至少指定供应商和设备，但不指定子系统。 首先列出包括的大多数信息的兼容 ID。

```cpp
{17ed6609-9bc8-44ca-8548-abb79b13781b}\ven_1&dev_2&rev_4 
{17ed6609-9bc8-44ca-8548-abb79b13781b}\ven_1&dev_2
```

 

 





