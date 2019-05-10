---
title: 驱动程序选择过程概述
description: 驱动程序选择过程概述
ms.assetid: 120ab9f9-6ac5-4b76-bee1-2e975d0c38f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fef4436d078e4fccb7d62e9968867e8bc8c4011
ms.sourcegitcommit: 3a51ae8db61be0e25549a5527ea3143e3025e82f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65456370"
---
# <a name="overview-of-the-driver-selection-process"></a>驱动程序选择过程概述


Windows 表示驱动程序，因为*驱动程序节点*，其中包括的设备，如任何服务、 特定于设备的共同安装程序和注册表项的所有软件支持。 设备服务包括功能驱动程序和任何较高级别和较低级别设备筛选器驱动程序。

某些设备需要专门为该设备或一个旨在支持一系列设备的供应商提供驱动程序而设计。 但是，其他设备可由系统提供驱动程序支持的所有设备的给定[设备安装程序类](device-setup-classes.md)。 Windows 将选择最符合设备的驱动程序。 如果 Windows 找不到这样的驱动程序，它将选择越来越多地更多常规驱动程序。

### <a href="" id="how-setup-searches-for-drivers"></a> Windows 搜索驱动程序的方式

Windows 搜索中的设备类型相匹配的驱动程序的特定位置。 驱动程序与设备相匹配，如果满足以下条件：

-   Plug and Play (PnP) 之一[设备标识字符串](device-identification-strings.md)，为其报告由总线驱动程序的设备与设备标识字符串中的匹配[ **INF*模型*部分**](inf-models-section.md)驱动程序的条目[INF 文件](overview-of-inf-files.md)。

-   如果匹配的设备标识字符串中[ **INF*模型*部分**](inf-models-section.md)条目指定*TargetOSVersion*修饰，修饰匹配设备已安装的操作系统版本。

    有关详细信息*TargetOSVersion*修饰，请参阅[结合使用的操作系统版本的平台扩展](combining-platform-extensions-with-operating-system-versions.md)。

有关 Windows 搜索匹配的驱动程序的位置的详细信息，请参阅[其中 Windows 搜索驱动程序](where-setup-searches-for-drivers.md)。

### <a href="" id="how-setup-ranks-drivers"></a> Windows 驱动程序的级别

Windows 创建的所有匹配的驱动程序列表，并为每个驱动程序分配排名。 Windows 表示使用大于或等于零的整数值的每个驱动程序的排名。

有关排序过程的详细信息，请参阅[如何 Windows Ranks Drivers](how-setup-ranks-drivers.md)。

从 Windows Vista 开始，Windows 还进行排名基于该驱动程序进行数字签名的驱动程序。 Windows 进行排名，如下所示基于数字签名的驱动程序：

-   如果[ **AllSignersEqual**组策略](allsignersequal-group-policy--windows-vista-and-later-.md)是已禁用，Windows 驱动程序级别使用与签名的驱动程序比更高版本的 Microsoft 签名进行签名的[Authenticode](authenticode.md)签名。 即使使用验证码签名进行签名的驱动程序，在所有其他方面，设备的更好地匹配项，会发生此排名。

-   如果[ **AllSignersEqual**组策略](allsignersequal-group-policy--windows-vista-and-later-.md)是启用了，Windows 同样排名数字签名的所有驱动程序。

**请注意**  从 Windows 7 开始[AllSignersEqual 组策略](allsignersequal-group-policy--windows-vista-and-later-.md)默认情况下启用。 在 Windows Vista 和 Windows Server 2008 **AllSignersEqual**组策略在默认情况下处于禁用状态。 IT 部门可以重写默认排名行为通过启用或禁用**AllSignersEqual**组策略。

 

从 Windows 签名颁发机构签名如下所示：

-   高级 Windows 硬件质量实验室 (WHQL) 签名和标准 WHQL 签名

-   收件箱驱动程序签名

-   Windows 可持续工程 (Windows SE) 签名

-   相同的 Windows 版本的 WHQL 签名或晚于[LowerLogoVersion](lowerlogoversion.md)驱动程序的设备安装程序类的值

### <a href="" id="how-setup-selects-drivers"></a> Windows 中如何选择驱动程序

Windows 选择作为设备的最佳匹配项的排名值最小的驱动程序。

但是，如果有多个同样排名的驱动程序的设备的最佳匹配项，Windows 使用驱动程序的日期和版本选择的驱动程序。 通过指定驱动程序的日期和版本[ **INF DriverVer 指令**](inf-driverver-directive.md)中的驱动程序包含[INF 文件](overview-of-inf-files.md)。

Windows 使用以下条件来选择设备驱动程序：

-   Windows 将选择具有最低的排名值作为设备的最佳匹配项的驱动程序。

-   对于具有相等的排名的驱动程序，Windows 会选择具有最新日期的驱动程序。

-   对于具有相等的秩和日期的驱动程序，Windows 会选择具有最高版本的驱动程序。

-   对于具有相等的排名、 日期和版本的驱动程序，Windows 可以选择任何驱动程序。

 

 





