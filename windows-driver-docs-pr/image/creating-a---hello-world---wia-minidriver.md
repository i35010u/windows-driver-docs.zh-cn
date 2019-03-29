---
title: 创建 Hello World WIA 微型驱动程序
description: 创建 Hello World WIA 微型驱动程序
ms.assetid: 074da2ff-bc60-48a9-b2ff-83f070bd5351
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caccf6323e26f54f18298efe760928a48680b337
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568631"
---
# <a name="creating-a-hello-world-wia-minidriver"></a>创建 Hello World WIA 微型驱动程序





此 WIA 微型驱动程序是一个简单的 DLL 导出两个函数，并实现三个 COM 接口。 下面的代码示例可以编译到工作 WIA 微型驱动程序。 此 WIA 微型驱动程序创建的项树具有根项，并且不能传输的数据，但它显示了获取 WIA 的驱动程序加载和运行所需的基础知识。

以下文件用于创建"Hello World"WIA 微型驱动程序：

*hellowld.def* − [Hello World 定义文件](--hello-world---definition-file.md)。

*hellowld.inf* − [Hello World 安装文件](--hello-world---installation-file.md)。

*hellowld.cpp* − [Hello World 实现文件](--hello-world---implementation-file.md)。

有关如何将自定义 UI 添加到微型驱动程序，请参阅，[创建"Hello World"WIA 微型驱动程序用户界面扩展](creating-a--hello-world--wia-minidriver-ui-extension.md)。

 

 




