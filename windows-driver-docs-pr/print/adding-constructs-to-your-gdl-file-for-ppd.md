---
title: 将构造添加到 PPD 的 GDL 文件
description: 将构造添加到 PPD 的 GDL 文件
keywords:
- 构造 WDK 打印机自动配置
- PPD 文件 WDK 自动配置，构造
- 内置自动配置支持 WDK 打印机、构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd312ed182a98567c2392fb62284f6411432373f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794233"
---
# <a name="adding-constructs-to-your-gdl-file-for-ppd"></a>将构造添加到 PPD 的 GDL 文件


若要支持自动配置，必须使用以下新关键字将构造添加到 GDL 文件： \* **BidiQuery**、 \* *_QueryString_*、 \* *_BidiResponse_*、 \* *_ResponseType_*、 \* *_ResponseData_* 和 \* *_BidiValue_*。 您可以使用这些关键字指定与某一功能选项关联的双向架构请求，以及对该选项的可能响应。

\**_功能_* 构造可以包含单个 \* *_BidiQuery_* 构造，作为 \* *_查询字符串_* 实例的容器。 \**_功能_* 构造实例中的查询字符串是一个 Unicode 字符串，其中包含到要查询的功能的双向通信架构路径以及该功能的特定属性的名称。

\**_功能_* 构造还可以包含单个 \* *_BidiResponse_* 构造，该构造充当一个 \* *_ResponseType_* 实例和一个可选 \* *_ResponseData_* 实例的容器。

\*与功能构造关联的每个 *_选项_* 构造都 \* *_Feature_* 必须包含一个 \* *_BidiValue_* 实例，该实例包含适用于该选项的响应的字符串表示形式 \* *_Option_*。

下面的示例演示如何根据 PPD 文件中列出的功能，将相应的构造添加到 GDL 文件。 前两个示例包含一个 PPD 示例和一个 GDL 示例，其中包含支持自动检测或自动配置特定可安装功能所需的构造。 第三个示例为硬盘自动检测提供了 GDL 示例，并假定该硬盘驱动器存在 PPD 功能定义。

[自动检测 PPD 的双工单元](autodetect-the-duplex-unit-for-ppd.md)

[自动配置 PPD 的打印机内存](autoconfigure-the-printer-s-memory-for-ppd.md)

[自动检测 PPD 的打印机硬盘驱动器](autodetect-the-printer-s-hard-drive-for-ppd.md)

 

 




