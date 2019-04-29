---
title: AV/C 设备标识符
description: AV/C 设备标识符
ms.assetid: c2d108c7-5ea9-42c1-92d7-5ba90f2f4232
keywords:
- AV/C WDK 标识符
- 标识符 WDK AV/C
- 设备 Id WDK AV/C
- Avc.sys 功能驱动程序 WDK，标识符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d10ce9df44cef5b42d05f81ef48cc3667eeee9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384807"
---
# <a name="avc-device-identifiers"></a>AV/C 设备标识符





当用户连接到计算机，AV/C 设备*Avc.sys*枚举在设备上活动的子单元连接，并为其生成的设备标识符 (ID) 字符串。 没有为每个活动的子单元 AV/C 的设备中的设备标识符。 如果有任何活动的子单元连接 AV/C 的设备中, 然后*Avc.sys*生成 AV/C 设备本身的设备标识符。

对等子单元连接的设备标识符字段的格式为：

**AVC\\*Vendor*&*Model*&*SubunitType*&*SubunitID***

虚拟子单元连接的设备标识符字段的格式为：

**VAVC\\*Vendor*&*Model*&*SubunitType*&*SubunitID***

在其中使用数字字段中，将数字转换为十六进制，和 alpha 字符转换为大写。 没有前导零。 该驱动程序的 INF 文件中指定的设备标识符必须与匹配此格式。 硬件标识符和兼容的标识符中的所有数值字段都标记，如下所示 （有例外，如下所述）：

-   ***供应商***：**即使\_** （除非供应商文本可用）

-   ***模型***:**MOD\_**  （除非模型文本可用）

-   ***SubunitType***:**TYP\_**

-   ***SubunitID***:**ID\_**

*Avc.sys*创建每个活动的子单元外部 C AV/设备上存在一个设备对象。 添加或删除从 IEEE 1394 总线 AV/C 设备时，将触发 IEEE 1394 总线重置。 *Avc.sys*然后重新枚举所有活动的子单元连接 AV/C 的设备。 重新枚举允许重新配置其自己要添加或删除子单元连接，而无需重新加载的 Windows 设备*Avc.sys*每次 AV/C 设备的操作系统时切换模式。 例如，相机模式和 VTR 模式之间切换 DV 摄像机时，将应用此功能。 因此，子单元驱动程序加载和卸载仅在添加和删除其相应的活动子单元连接。

*Avc.sys*无法区分多个子单元连接的相同***SubunitType***，因此添加和删除这些子单元连接加载和卸载相应的子单元驱动程序最高***SubunitID***.

每个次级单位的设备对象具有一个或两个硬件标识符和多个兼容的标识符。 供应商必须提供一个或多个这些硬件或兼容的标识符，其子单元驱动程序的 INF 文件中，如下所述。 Windows 使用这些设备标识符来找到合适的驱动程序加载每个设备连接到计算机的子单元第一次。 你可以检查 Microsoft 提供*61883.inf*， *Msdv.inf*并*Mstape.inf*硬件和 AV/C 的设备的兼容的设备标识符的示例文件。 有关实现 INF 文件的详细信息，请参阅[INF 文件的部分和指令](https://msdn.microsoft.com/library/windows/hardware/ff547433)。

设备标识符字符串的各个元素如下所示：

<a href="" id="vendor"></a>***供应商***  
如果供应商名称文本是 IEEE 1394 配置 ROM 单元功能根目录中存在，则中使用供应商名称文本***供应商***字段。 例如：

**AVC\\Microsoft&*Model*&*SubunitType*&*SubunitID***

否则，供应商的唯一编号 （如分配通过 IEEE 1394 贸易协会） 中使用***供应商***字段。 在以下示例中，"50F2"是 Microsoft 的 1394TA 供应商编号：

**AVC\\VEN\_50F2&*Model*&*SubunitType*&*SubunitID***

如果供应商名称文本不存在，则从该模块获取的数值\_供应商\_ID IEEE 1394 配置 ROM 的根目录中的条目。 命令和此即时项的状态注册 (CSR) 体系结构密钥是 0316 （十六进制），剩余的 24 位是数值模块\_供应商\_ID 条目。

<a href="" id="model"></a>***模型***  
如果模型名称文本中不存在，IEEE 1394 配置 ROM 单元功能，则中使用模型名称文本***模型***字段。 例如：

**AVC\\Microsoft&DVCamcorder&*SubunitType*&*SubunitID***

否则，在使用的型号***模型***字段。 例如：

**AVC\\Microsoft&MOD\_0&*SubunitType*&*SubunitID***

使用的 1394年配置 ROM 单元目录中的模型文本，使单元目录项的优先级。 优先顺序如下所示：

1.  单元目录中的数字标识符。

2.  根目录中的模型文本。

3.  根目录中的模型标识符。

<a href="" id="subunittype"></a>***SubunitType***  
如果可用，请***SubunitType***字段是从子单元地址中提取并转换为十六进制值为每个字节的字符串。 仅当已扩展的子单元类型有多个字节。 通常情况下，初始的字节从提取的地址字节，五个最高有效位的 5.3.3 节中所述*AV/C 数字接口命令设置常规规范、 Rev 3.0*。

例如：**AVC\\VEN\_50F2&MOD\_0&TYP\_4&*SubunitID***

子单元的列表类型， *Avc.sys*支持和其对应的数字值，请参阅[ **AvcSubunitType**](https://msdn.microsoft.com/library/windows/hardware/ff554137)。

<a href="" id="subunitid"></a>***SubunitID***  
如果***SubunitType***字段将可用， ***SubunitID***字段也是可用。 当*Avc.sys*查询 AV/C 设备中的子单元信息，设备响应的每种类型的子单元连接数量。 此从零开始计数用于创建每个次级单位的设备标识符。 子单元地址规范还允许***SubunitID***字段被扩展，但这一方面隐藏来自子单元驱动程序 （和从您的 INF 文件的作者）。 在所有情况下使用的从零开始的实例编号。 例如，如果***SubunitID***字段已扩展为支持 270 子单元连接，270th 子单元具有 10 个 D (269 十进制) 的子单元标识符。 例如：

**AVC\\Microsoft&MOD\_0&TYP\_4&ID\_10D**

对于不提供的 AV/C 单元***SubunitType***或***SubunitID***，设备标识符字符串然后组成仅***供应商***和***模型***字段，没有尾随 and 符 (&)。

 

 




