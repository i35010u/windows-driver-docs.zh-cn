---
title: 查找和管理硬件提交内容
description: 了解如何通过搜索文本或选择关键字搜索中的驱动程序属性来查找特定的 Windows 硬件提交内容。
ms.topic: article
ms.date: 09/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 19f8a7f74a143e93f1cf49d2e1007f0c6be65e7c
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "81679115"
---
# <a name="find-a-hardware-submission"></a>查找硬件提交

组织提交的所有硬件提交内容将显示在硬件仪表板的“驱动程序”页上。  若要查找特定的硬件提交内容，可执行以下搜索：

- 纯文本搜索

- 驱动程序属性关键字搜索

## <a name="plain-text-search"></a>纯文本搜索

可在文本框中输入任何搜索短语。 仪表板将返回所需的条目，其中包含与以下任何字段中的短语匹配的单词：

- 产品 ID（专用和共享）

- 提交 ID

- 产品名称

- 提交名称

- 硬件 ID

- INF 名称

- 操作系统代码

例如，搜索短语 **mydriver** 会返回包含产品名称 *mydriver 1*、*new mydriver*、*old mydriver 2*、*mydriver1* 和 *mydriver_new* 的提交内容。

## <a name="keyword-search"></a>关键字搜索

可以使用关键字搜索按驱动程序属性搜索驱动程序。 在搜索框中键入 **\@** 符号时，仪表板会显示可用属性的列表。 

![硬件仪表板中的“驱动程序”页屏幕截图，其中显示文本框中输入了 @ 符号。 可用属性列表将显示在 @ 符号下面。](images/ampersand-search.png)

在 @ 符号后面输入文本时，列表范围将缩小为与该条件匹配的内容。 单击某个预填充的值时，该值会以 **(@*ParameterName*: "")** 格式显示在搜索框中。 不要修改参数名称或格式，只能在引号 ( **""** ) 之间输入字符串。 搜索短语可以是完整或不完整的搜索值。 例如，若要按操作系统代码搜索驱动程序，可以使用：

**@OperatingSystemCode:"Windows 10 RS4 Client x64"** 

、

**@OperatingSystemCode:"Windows 10 RS4"**

还可以使用多个属性进行搜索。 使用多个属性就如同将它们包含在 AND 运算符组合中一样。 例如，如果同时搜索产品名称和提交状态 ( **@ProductName:"test" @SubmissionStatus:"Failed"** )，则仪表板只返回与产品名称和提交状态**都**匹配的记录。

![硬件仪表板中的“驱动程序”页屏幕截图，其中输入了两个属性：@ProductName:"test" 和 @SubmissionStatus:"Failed"。 所有结果的产品名称中都包含“test”，并且提交状态中都包含“Failed”。](images/two-attribute-search.png)

可使用以下驱动程序属性执行关键字搜索：

|参数|类型|可能值|
|----|----|----|
|ProductID |数字|17 位专用产品 ID|
|SharedProductID |数字|19 位共享产品 ID|
|ProductName |文本|
|CertificationType |文本|Attestation、HCK、HLK、WLK|
|权限 |文本|Author、Publisher|
|SubmissionID |数字|19 位提交 ID|
|SubmissionName |文本|
|SubmissionType |文本|Initial、Derived|
|SubmissionStatus |文本|Complete、Failed、NotSet、Processing、Ready|
|IsExtensionDriver |布尔|False、True|
|IsUniversalDriver |布尔|False、True|
|IsDeclarativeDriver |布尔|False、True|
|INFName |文本|
|HardwareID |文本|
|OperatingSystemCode |文本|[OS 代码列表](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-product-data#list-of-operating-system-codes)|

## <a name="search-results"></a>搜索结果

显示在仪表板上的搜索结果将列出与搜索短语匹配的驱动程序提交内容。

> [!NOTE]
> 只有在包验收完成后，硬件仪表板才会创建实体。 因此，只有在包验收完成后，驱动程序提交内容才会显示在搜索结果中。

在结果中，单击“专用产品 ID”可导航到该驱动程序的概述页。  在该页中，可以查看有关驱动程序提交内容的信息、通过 [DUA 过程](https://docs.microsoft.com/windows-hardware/test/hlk/user/create-a-driver-only-update-package)更新提交内容，以及查看、创建和编辑发货标签或下载已签名的文件。

### <a name="important-points"></a>要点

1. 在关键字搜索中只能使用给定的参数一次。 例如，搜索 ( **@ProductName:"test" @ProductName:"system"** ) 会导致出错。

2. 目前，无法使用参数“提交内容创建日期”或“源”进行搜索。   目前不可使用这些参数。

3. 默认情况下，搜索结果按“提交内容创建日期”的降序排序。  可以单击任一列标题字段来更改排序。

4. 若要搜索产品名称或硬件 ID，请使用完整的搜索字符串。 如果需要对这些字段使用通配符运算符，请避免使用特殊字符（非字母或数字的字符）。
