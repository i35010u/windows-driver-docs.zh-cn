---
title: AV/C 设备标识符
description: AV/C 设备标识符
ms.assetid: c2d108c7-5ea9-42c1-92d7-5ba90f2f4232
keywords:
- AV/C WDK，标识符
- 标识符 WDK AV/C
- 设备 Id WDK AV/C
- Avc 函数驱动程序 WDK，标识符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99e935f243adab28b4337a82853e06147247010d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843364"
---
# <a name="avc-device-identifiers"></a>AV/C 设备标识符





当用户将 AV/C 设备连接到计算机时， *Avc*将枚举设备上的活动子单元连接，并为其生成设备标识符（ID）字符串。 AV/C 设备中的每个活动子单位都有一个设备标识符。 如果 AV/C 设备中没有活动的子单元连接，则*Avc*将为 Av/c 设备本身生成设备标识符。

对等子单元连接的设备标识符字段的格式为：

**AVC\\*供应商*&*型号*&*SubunitType*& * SubunitID***

用于虚拟子单元连接的设备标识符字段的格式为：

**VAVC\\*供应商*&*型号*&*SubunitType*& * SubunitID***

在使用数字的字段中，数字转换为十六进制，而字母字符转换为大写形式。 没有前导零。 驱动程序的 INF 文件中指定的设备标识符必须与此格式匹配。 硬件标识符和兼容标识符中的所有数字字段都被标记为以下内容（有例外，如所述）：

-   ***供应商***：**即使\_** （除非供应商文本可用）

-   ***模型***： **MOD\_** （除非模型文本可用）

-   ***SubunitType***： **TYP\_**

-   ***SubunitID***： **ID\_**

*Avc*为外部 AV/C 设备上存在的每个活动的子单位创建设备对象。 每当在 IEEE 1394 总线中添加或删除 AV/C 设备时，都会触发 IEEE 1394 总线重置。 然后， *Avc*将在所有连接的 AV/C 设备上重新枚举活动的子单元连接。 重新枚举允许设备自行重新配置以添加或删除子单元连接，而无需在每次切换 AV/C 设备的操作模式时重新加载*Avc* 。 例如，当 DV 摄像机在相机模式和 VTR 模式之间切换时，此功能适用。 因此，仅当添加并删除了子单位的相应活动子单元连接时，才会加载和卸载子工作驱动器。

*Avc*无法区分同一***SubunitType***的多个子单元连接，因此添加和删除这些子单元连接会加载并卸载具有最高***SubunitID***的相应子单位驱动程序。

每个次级的设备对象有一个或两个硬件标识符和多个兼容的标识符。 供应商必须为其子单位驱动程序提供一个或多个这些硬件或兼容标识符，如下所述。 当设备第一次连接到计算机时，Windows 将使用这些设备标识符来查找要为每个次级计算机加载的合适的驱动程序。 您可以查看 Microsoft 提供的*61883*、 *Msdv*和*Mstape*文件，以了解用于 AV/C 设备的硬件和兼容设备标识符的示例。 有关实现 INF 文件的详细信息，请参阅[INF 文件部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)。

设备标识符字符串的各个元素如下所示：

<a href="" id="vendor"></a>***采购***  
如果供应商名称文本出现在 IEEE 1394 配置 ROM 的单元功能根目录中，则供应商名称文本用于***供应商***字段。 例如：

**AVC\\Microsoft &*型号*&*SubunitType*& * SubunitID***

否则 ***，供应商字段中***将使用供应商的唯一编号（由 IEEE 1394 贸易协会分配）。 在下面的示例中，"50F2" 是 Microsoft 的1394TA 供应商编号：

**AVC\\即使\_50F2 &*模型*&*SubunitType*& * SubunitID***

如果供应商名称文本不存在，则将在 IEEE 1394 配置 ROM 的根目录中从模块\_供应商\_ID 条目获取数值。 此即时项的命令和状态注册（CSR）体系结构密钥为0316（十六进制），而剩余的24位为数值模块\_供应商\_ID 条目。

<a href="" id="model"></a>***模式***  
如果模型名称文本出现在 IEEE 1394 配置 ROM 的单位功能中，则模型名称文本用于 "***模型***" 字段。 例如：

**AVC\\Microsoft & DVCamcorder &*SubunitType*& * SubunitID***

否则，将在 "***模型***" 字段中使用模型号。 例如：

**AVC\\Microsoft & MOD\_0 &*SubunitType*& * SubunitID***

使用来自1394配置 ROM 单元目录的模型文本，并将其优先级设置为单元目录条目。 优先顺序如下：

1.  单元目录中的数值标识符。

2.  根目录中的模型文本。

3.  根目录中的模型标识符。

<a href="" id="subunittype"></a>***SubunitType***  
如果可用， ***SubunitType***字段将从子单位地址提取，并转换为每个字节的十六进制值字符串。 只有在已扩展了子类型的情况时，才有多个字节。 通常，初始字节从地址字节的五个最高有效位提取，如*AV/C 数字接口命令集常规3.0 规范*的5.3.3 部分中所述。

例如： **AVC\\即使\_50F2 & MOD\_0 & TYP\_4 & * SubunitID***

有关*Avc*支持的子类型和其对应数值的列表，请参阅[**AvcSubunitType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcsubunittype)。

<a href="" id="subunitid"></a>***SubunitID***  
如果 " ***SubunitType*** " 字段可用，则 " ***SubunitID*** " 字段也可用。 当*Avc*查询 AV/C 设备的子单位信息时，设备将以每个类型的子单元连接计数进行响应。 此从零开始的计数用于创建每个次级的设备标识符。 子单位地址规范还允许对***SubunitID***字段进行扩展，但是，子单位驱动程序（以及 INF 文件的作者）将隐藏此方面。 所有情况下都使用从零开始的实例编号。 例如，如果 " ***SubunitID*** " 字段已扩展为支持270子单元连接，则270th 子区域的子单位标识符为 now-10d （269 decimal）。 例如：

**AVC\\Microsoft & MOD\_0 & TYP\_\_Now-10d**

对于不提供***SubunitType***或***SubunitID***的 AV/C 单元，设备标识符字符串只包含***供应商***和***模型***字段，没有尾随符号（&）。

 

 




