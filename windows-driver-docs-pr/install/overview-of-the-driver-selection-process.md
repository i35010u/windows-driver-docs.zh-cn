---
title: 驱动程序选择过程概述
description: 驱动程序选择过程概述
ms.assetid: 120ab9f9-6ac5-4b76-bee1-2e975d0c38f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 216ab565c6ebf0e65062aa7cc5ba5df3e720949e
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095891"
---
# <a name="overview-of-the-driver-selection-process"></a>驱动程序选择过程概述


Windows 将驱动程序表示为 *驱动程序节点*，其中包括设备的所有软件支持，如任何服务、设备特定的共同安装程序和注册表项。 设备的服务包括功能驱动程序和任何高级和低级别的设备筛选器驱动程序。

某些设备需要专用于该设备的供应商提供的驱动程序，或者设计为支持一系列设备的驱动程序。 但是，其他设备可能由系统提供的驱动程序驱动，该驱动程序支持给定 [设备安装程序类](./overview-of-device-setup-classes.md)的所有设备。 Windows 选择与设备最匹配的驱动程序。 如果 Windows 找不到这样的驱动程序，它将从更通用的驱动程序中进行选择。

### <a name="how-windows-searches-for-drivers"></a><a href="" id="how-setup-searches-for-drivers"></a> Windows 如何搜索驱动程序

Windows 在特定位置中搜索与设备匹配的驱动程序。 如果满足以下条件，则驱动程序将匹配设备：

-   设备的总线驱动程序报告的即插即用 (PnP) [设备标识字符串](device-identification-strings.md)之一与该驱动程序[inf 文件](overview-of-inf-files.md)的 " [**inf*模型*" 部分**](inf-models-section.md)条目中的设备标识字符串匹配。

-   如果 " [**INF *模型* " 部分**](inf-models-section.md) 条目中的匹配设备标识字符串指定了 *TargetOSVersion* 装饰，则该修饰将与要安装设备的操作系统版本匹配。

    有关 *TargetOSVersion* 修饰的详细信息，请参阅将 [平台扩展与操作系统版本结合起来](combining-platform-extensions-with-operating-system-versions.md)。

有关 Windows 在何处搜索匹配驱动程序的详细信息，请参阅 [Windows 搜索驱动程序的位置](./how-windows-selects-a-driver-for-a-device.md)。

### <a name="how-windows-ranks-drivers"></a><a href="" id="how-setup-ranks-drivers"></a> Windows 排名驱动程序的方式

Windows 将创建一个列表，其中列出了所有匹配驱动程序，并为每个驱动程序指定了排名。 Windows 使用大于或等于零的整数值表示每个驱动程序的排名。

有关排名过程的详细信息，请参阅 [Windows 如何对驱动程序进行排名](how-setup-ranks-drivers--windows-vista-and-later-.md)。

从 Windows Vista 开始，Windows 还根据驱动程序是否已进行数字签名来对驱动程序进行排名。 Windows 基于数字签名对驱动程序进行排名，如下所示：

-   如果[ **AllSignersEqual**组策略](./allsigningequal-group-policy.md)处于禁用状态，则 Windows 将使用 Microsoft 签名进行签名的驱动程序高于使用[Authenticode](authenticode.md)签名进行签名的驱动程序。 即使使用 Authenticode 签名签名的驱动程序在所有其他方面都是更好地匹配设备，也会出现此排名。

-   如果启用了[ **AllSignersEqual**组策略](./allsigningequal-group-policy.md)，则 Windows 将对所有数字签名的驱动程序进行平均排名。

**注意**   从 Windows 7 开始，默认情况下启用[AllSignersEqual 组策略](./allsigningequal-group-policy.md)。 在 Windows Vista 和 Windows Server 2008 中，默认情况下， **AllSignersEqual** 组策略处于禁用状态。 IT 部门可以通过启用或禁用 **AllSignersEqual** 组策略来覆盖默认排名行为。

 

Windows 签名颁发机构的签名包括：

-   高级 Windows 硬件质量实验室 (WHQL) 签名和标准 WHQL 签名

-   收件箱驱动程序的签名

-   Windows (Windows SE) 签名的 windows 持续工程设计

-   Windows 版本的 WHQL 签名，该签名与驱动程序的设备安装程序类的 [LowerLogoVersion](lowerlogoversion.md) 值相同或更高版本

### <a name="how-windows-selects-drivers"></a><a href="" id="how-setup-selects-drivers"></a> Windows 如何选择驱动程序

Windows 将选择具有最低排名值的驱动程序作为设备的最佳匹配项。

但是，如果有多个平均排名的驱动程序是设备的最佳匹配项，Windows 将使用该驱动程序的日期和版本来选择驱动程序。 驱动程序的日期和版本由驱动程序的[inf 文件](overview-of-inf-files.md)中包含的[**inf DriverVer 指令**](inf-driverver-directive.md)指定。

Windows 使用以下条件来选择设备驱动程序：

-   Windows 将选择具有最低排名值的驱动程序作为设备的最佳匹配项。

-   对于排名相同的驱动程序，Windows 将选择具有最近日期的驱动程序。

-   对于排名和日期相同的驱动程序，Windows 将选择具有最高版本的驱动程序。

-   对于排名、日期和版本相同的驱动程序，Windows 可以选择任何驱动程序。

 

