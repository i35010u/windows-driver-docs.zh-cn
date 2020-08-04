---
title: 使用计算机硬件 ID (CHID)
description: 计算机硬件 ID (CHID) 在“为计算机指定硬件 ID”中定义。
ms.assetid: 45DCAED5-8D20-4A31-B316-0460AB030DAD
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3bb465ae25376fd1b8ff0ffe88c7607d3543f05
ms.sourcegitcommit: f63852446e614c985a65f599cdfe788bdb0c6089
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2020
ms.locfileid: "87425722"
---
# <a name="using-computer-hardware-ids-chids"></a>使用计算机硬件 ID (CHID)

计算机硬件 ID (CHID) 在[为计算机指定硬件 ID](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-hardware-ids-for-a-computer) 中定义。

Windows 10 添加多个合并基板制造商和基板产品信息的新 CHID。 这些新 CHID 包含在 CHID 层次结构中，如下表所示。 此表以特异性的降序顺序显示该层次结构。 Windows 10 中新添加的 CHID 以粗体突出显示。

|HWID|目录|
|----|----|
|HardwareID-0|制造商 + 系列 + 产品名称 + SKU 号 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本|
|HardwareID-1|制造商 + 系列 + 产品名称 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本|
|HardwareID-2|制造商 + 产品名称 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本|
|HardwareID-3|**制造商 + 系列 + 产品名称 + SKU 号 + Baseboard_Manufacturer + Baseboard_Product**|
|HardwareID-4|制造商 + 系列 + 产品名称 + SKU 号|
|HardwareID-5|制造商 + 系列 + 产品名称|
|HardwareID-6|**制造商 + SKU 号 + Baseboard_Manufacturer + Baseboard_Product**|
|HardwareID-7|制造商 + SKU 号|
|HardwareID-8|**制造商 + 产品名称 + Baseboard_Manufacturer + Baseboard_Product**|
|HardwareID-9|制造商 + 产品名称|
|HardwareID-10|**制造商 + 系列 + Baseboard_Manufacturer + Baseboard_Product**|
|HardwareID-11|制造商 + 系列|
|HardwareID-12|制造商 + 机箱类型|
|HardwareID-13|**制造商 + Baseboard_Manufacturer + Baseboard_Product**|
|HardwareID-14|制造商|

OEM 必须向驱动程序发布者提供正确的 CHID 信息。 包含在 Windows 桌面工具 SDK 中的 [ComputerHardwareIds](https://docs.microsoft.com/windows-hardware/drivers/devtest/computerhardwareids) 工具有助于从一组已知的系统管理 BIOS (SMBIOS) 值中报告 CHID。 ComputerHardwareIds 执行两个不同的任务。

1. 默认行为：该工具报告系统的 SMBIOS 值和生成的 CHID。

   默认情况下，该工具显示系统的 SMBIOS 值以及从 SMBIOS 值中生成的 CHID。

2. 模拟行为：该工具从用户提供的 SMBIOS 值中生成 CHID。

   可使用模拟 SMBIOS 值（例如制造商、系列和 SKU）运行该工具，以获取生成的 CHID 列表。 这允许你确定将在带有特定 SMBIOS 数据值的系统上生成哪些 CHID。

## <a name="tips-for-consistent-chids"></a>一致 CHID 的提示

CHID 基于区分大小写的 SMBIOS 值生成。 必须小心地确保系统不在 SMBIOS 文本值中混合大小写。 同样，不特殊处理 UNICODE 字符。 区别对待特殊字符的大写和小写版本，如土耳其语的带点和不带点的字母 I：I、ı、İ 和 i 是不同的。

ComputerHardwareIds 工具仅计算提供必要的 SMBIOS 值的 CHID。 如果缺少 SMBIOS 数据字段（或为空），不会生成任何相关的 CHID。 例如，如果 SMBIOS SKU 字段为空，CHID 0、3、4、6 和 7 将不可用于该特定系统。

有关 CHID 的详细信息，请参阅[指定计算机的硬件 ID](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-hardware-ids-for-a-computer)。

## <a name="how-the-windows-update-service-uses-chid"></a>Windows 更新服务如何使用 CHID

Windows 更新服务使用 CHID 来“减少驱动程序适用的的系统的数目”。  在进行 PnP 分级之前，首先会进行这样的缩减操作。

Windows 更新服务根据已安装的 Windows OS 级别对 CHID 进行不同的处理。  

|Windows 10 版本|Windows 更新行为|
|----|----|
|1507 到 1703|Windows 更新将每个 CHID 分为从 CHID-0 到 CHID-14 的几级，其中，CHID-0 的级别高于 CHID-14|
|1709 及更高版本|CHID 不再分级。 从 CHID-0 到 CHID-14 的所有适用的 CHID 目标驱动程序将分组到一起，然后对整个组进行 PnP 分级。|

请考虑以下示例：

Contoso 将以下两个驱动程序发布为“自动”，它们针对同一 HWID，但 CHID 不同。  

- 发行版 1 - 面向 CHID-4（制造商 + 系列 + 产品名称 + SKU 编号）

- 发行版 2 - 面向 CHID-5（制造商 + 系列 + 产品名称）

对于与 CHID-5 匹配的系统，Windows 更新服务会选择哪一个？

|Contoso 系统|Windows OS 级别|提供的驱动程序|
|----|----|----|
|与 CHID-5 匹配，但与 CHID-4 不匹配|Windows 10 1703 或更低版本|分发 2|
|与 CHID-5 匹配，但与 CHID-4 不匹配|Windows 10 1709 或更高版本|分发 2|
|与 CHID-5 匹配，**且**与 CHID-4 匹配|Windows 10 1703 或更低版本|分发 1|
|与 CHID-5 匹配，**且**与 CHID-4 匹配|Windows 10 1709 或更高版本|二者都提供。   然后，PnP 分级会选择这二者中的最佳匹配进行安装。|
