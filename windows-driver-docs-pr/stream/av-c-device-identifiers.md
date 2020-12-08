---
title: AV/C 设备标识符
description: AV/C 设备标识符
keywords:
- AV/C WDK，标识符
- 标识符 WDK AV/C
- 设备 Id WDK AV/C
- Avc.sys 函数驱动程序 WDK，标识符
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4b1f8db9202dc0bd53ab3b4dc3e585a997c580f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801241"
---
# <a name="avc-device-identifiers"></a>AV/C 设备标识符

当用户将 AV/C 设备连接到计算机时， *Avc.sys* 枚举设备上的活动子单元连接，并为其生成设备标识符 (ID) 字符串。 AV/C 设备中的每个活动子单位都有一个设备标识符。 如果 AV/C 设备中没有活动的子单元连接，则 *Avc.sys* 为 Av/c 设备本身生成设备标识符。

对等子单元连接的设备标识符字段的格式为：

**AVC \\ *供应商* & *型号* & *SubunitType*& * SubunitID***

用于虚拟子单元连接的设备标识符字段的格式为：

**VAVC \\ *供应商* & *型号* & *SubunitType*& * SubunitID***

在使用数字的字段中，数字转换为十六进制，而字母字符转换为大写形式。 没有前导零。 驱动程序的 INF 文件中指定的设备标识符必须与此格式匹配。 硬件标识符和兼容标识符中的所有数字字段都标记为以下 (例外，如) 所述：

- **_供应商_*_： _* 即使 \_** (，除非供应商文本可用) 

- **_Model_*_： _* MOD \_** (，除非模型文本可用) 

- **_SubunitType_*_： _* TYP\_**

- **_SubunitID_*_： _* ID\_**

*Avc.sys* 为外部 AV/C 设备上存在的每个活动的子单位创建设备对象。 每当在 IEEE 1394 总线中添加或删除 AV/C 设备时，都会触发 IEEE 1394 总线重置。 然后 *Avc.sys* 在所有连接的 AV/C 设备上重新枚举活动的子单元连接。 重新枚举允许设备自行重新配置，以添加或删除子单元连接，而无需在每次打开 AV/C 设备的运行模式时重新加载 *Avc.sys* 。 例如，当 DV 摄像机在相机模式和 VTR 模式之间切换时，此功能适用。 因此，仅当添加并删除了子单位的相应活动子单元连接时，才会加载和卸载子工作驱动器。

*Avc.sys* 无法区分同一 ***SubunitType** _ 的多个子单元连接，因此添加和删除这些子单元连接将加载并卸载具有最高 _*_SubunitID_*_ 的相应子单位驱动程序。

每个次级的设备对象有一个或两个硬件标识符和多个兼容的标识符。 供应商必须为其子单位驱动程序提供一个或多个这些硬件或兼容标识符，如下所述。 当设备第一次连接到计算机时，Windows 将使用这些设备标识符来查找要为每个次级计算机加载的合适的驱动程序。 您可以查看 Microsoft 提供的 _61883 *、 *Msdv* 和 *Mstape* 文件，以了解用于 AV/C 设备的硬件和兼容设备标识符的示例。 有关实现 INF 文件的详细信息，请参阅查看 [Inf 文件部分](../install/inf-classinstall32-section.md) 和 [inf 文件指令](../install/inf-addcomponent-directive.md)。

设备标识符字符串的各个元素如下所示：

***供应商** _
  
如果供应商名称文本出现在 IEEE 1394 配置 ROM 的单元功能根目录中，则供应商名称文本用于 _*_供应商_*_ 字段。 例如：

_ *AVC \\ Microsoft&* Model *&* SubunitType *&* SubunitID * * * * *

否则，在 "*_供应商_* _" 字段中使用由 IEEE 1394 贸易协会) 指定的供应商唯一编号 (。 在下面的示例中，"50F2" 是 Microsoft 的1394TA 供应商编号：

_ *AVC \\ 即使 \_ 50F2&* 型号 *&* SubunitType *&* SubunitID * * *

如果供应商名称文本不存在，则从 \_ \_ IEEE 1394 配置 ROM 的根目录中的 "模块供应商 ID" 条目获取数值。 此立即条目 (CSR) 体系结构密钥的命令和状态注册为 0316 (十六进制) ，其余的24位为数值模块 \_ 供应商 \_ ID 条目。

**_模型_* _
  
如果模型名称文本出现在 IEEE 1394 配置 ROM 的单位功能中，则模型名称文本用于 " _*_模型_*_ " 字段。 例如：

_ *AVC \\ Microsoft&DVCamcorder&* SubunitType *&* SubunitID * * *

否则，将在 "*_模型_* _ _" 字段中使用模型号。 例如：

_ *AVC \\ MICROSOFT&MOD \_ 0&* SubunitType *&* SubunitID * * * * *

使用来自1394配置 ROM 单元目录的模型文本，并将其优先级设置为单元目录条目。 优先顺序如下：

1. 单元目录中的数值标识符。

1. 根目录中的模型文本。

1. 来自根目录的模型标识符。

**_SubunitType_* _
  
如果可用， _*_SubunitType_*_ 字段将从子单位地址提取，并转换为每个字节的十六进制值字符串。 只有在已扩展了子类型的情况时，才有多个字节。 通常，初始字节从地址字节的五个最高有效位提取，如 _AV/C 数字接口命令集常规3.0 规范的5.3.3 部分中所述。

例如： **AVC \\ 即使 \_ 50F2&MOD \_ 0&TYP \_ 4& * SubunitID***

有关 *Avc.sys* 支持的子类型和其对应数值的列表，请参阅 [**AvcSubunitType**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcsubunittype)。

**_SubunitID_* _
  
如果 " _*_SubunitType_*_ " 字段可用，则 " _*_SubunitID_*_ " 字段也可用。 当 _Avc.sys * 在 AV/C 设备中查询其子单位信息时，设备将以每个类型的子单元连接的计数进行响应。此从零开始的计数用于创建每个次级的设备标识符。子单位地址规范还允许对 ***SubunitID**_ 字段进行扩展，但是，从子单位驱动程序隐藏此方面 (，而从您的 INF 文件的作者) 。 所有情况下都使用从零开始的实例编号。 例如，如果 " _*_SubunitID_*_ " 字段已扩展为支持270子单元连接，则270th 子区域的 "子区域标识符" now-10d (269 decimal) 。 例如：

_ *AVC \\ MICROSOFT&MOD \_ 0&TYP \_ 4&ID \_ now-10d**

对于不提供 **_SubunitType_*_ 或 _*_SubunitID_ _ 的 AV/C 单元 *，设备标识符字符串只包含 _*_供应商_*_ 和 _*_模型_** 字段，无尾随符号 ( # A0) 。
