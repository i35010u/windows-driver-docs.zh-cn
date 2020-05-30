---
title: 创建 "Hello World" WIA 微型驱动程序
description: 创建 "Hello World" WIA 微型驱动程序
ms.assetid: 074da2ff-bc60-48a9-b2ff-83f070bd5351
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 22ff8de6891fba6bb0ed7213b5ba497e43aa15f9
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223568"
---
# <a name="creating-a-hello-world-wia-minidriver"></a>创建 "Hello World" WIA 微型驱动程序

此 WIA 微型驱动程序是一个简单的 DLL，它导出两个函数并实现三个 COM 接口。 下面的代码示例可以编译为一个工作的 WIA 微型驱动程序。 此 WIA 微型驱动程序创建的项树只有根项并且无法传输数据，但它显示了加载 WIA 驱动程序并使其正常运行所需的基础知识。

以下文件用于创建 "Hello World" WIA 微型驱动程序：

*hellowld* − ["Hello World" 定义文件](--hello-world---definition-file.md)。

*hellowld* − ["Hello World" 安装文件](--hello-world---installation-file.md)。

*hellowld* − ["Hello World" 实现文件](--hello-world---implementation-file.md)。

有关如何将自定义 UI 添加到微型驱动程序的信息，请参阅[创建 "Hello World" WIA 微型驱动程序 UI 扩展](creating-a--hello-world--wia-minidriver-ui-extension.md)。
