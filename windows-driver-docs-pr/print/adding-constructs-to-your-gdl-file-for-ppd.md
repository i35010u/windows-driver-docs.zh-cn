---
title: 将构造添加到 PPD 的 GDL 文件
description: 将构造添加到 PPD 的 GDL 文件
ms.assetid: 981952b2-cc13-4c62-935b-74e749278c0f
keywords:
- 构造 WDK 打印机自动配置
- PPD 文件 WDK 自动配置构造
- 框中自动配置支持 WDK 打印机，构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30b89bc0f78ffcca00337410f1144a2c7d43e924
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343231"
---
# <a name="adding-constructs-to-your-gdl-file-for-ppd"></a>将构造添加到 PPD 的 GDL 文件


若要支持自动配置，您必须构造到 GDL 文件使用添加以下新关键字：\***BidiQuery**， \* **QueryString**， \* **BidiResponse**， \* **ResponseType**， \* **ResponseData**，并\* **BidiValue**。 这些关键字可用于指定与一个选择一项功能，并对该选项的可能响应相关联的 bidi 架构请求。

一个\***功能**构造可以包含一个\* **BidiQuery**构造，它可作为一个用于\* **QueryString**实例。 中的查询字符串\***功能**构造实例是它包含具有特定属性的名称追加正被查询的功能的双向通信架构路径的 Unicode 字符串功能。

一个\***功能**构造还可以包含单个\* **BidiResponse**构造，其中一个充当容器\* **ResponseType**实例和一个可选\* **ResponseData**实例。

每个\***选项**与之关联的构造\***功能**构造必须包含\* **BidiValue**实例包括适用于的响应的字符串表示形式\***选项**。

以下示例演示如何将适当构造添加到你 GDL 文件中，基于 PPD 文件中列出的功能。 前两个示例包含 PPD 示例和支持自动检测或自动配置的特定安装的功能所需的构造 GDL 示例。 第三个示例的硬盘驱动器时，自动检测提供了一个 GDL 示例，并假定硬盘驱动器 PPD 功能定义的存在。

[自动检测 PPD 双面打印单元](autodetect-the-duplex-unit-for-ppd.md)

[自动配置 PPD 的打印机的内存](autoconfigure-the-printer-s-memory-for-ppd.md)

[自动检测打印机的硬推动 PPD](autodetect-the-printer-s-hard-drive-for-ppd.md)

 

 




