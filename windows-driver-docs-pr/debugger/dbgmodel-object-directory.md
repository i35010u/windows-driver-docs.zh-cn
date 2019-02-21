---
title: 调试器数据模型的目录对象
description: 目录对象表示和操作的文件系统上的目录。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: c6ef217cee7a0cc28fd803e7e32ae2fd0249b46c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533807"
---
# <a name="directory-objects"></a>目录对象 
## <a name="summary"></a>摘要
目录对象表示和操作的文件系统上的目录。

## <a name="object-methods"></a>对象方法
|名称|返回类型|签名|描述|
|--- |-- |--- |--- |
|CreateFile|[file](dbgmodel-object-file.md)|CreateFile(relativePath, [disposition])|与给定的处理设置创建该目录中的文件。 处置可能"OpenExisting"、"CreateNew"或"CreateAlways"之一。|
|CreateSubDirectory|[directory](dbgmodel-object-directory.md)|CreateSubDirectory(name)|创建新的子目录的目录中。|
|删除||Delete （)|如果为空，则删除子目录。|
|OpenFile|[file](dbgmodel-object-file.md)|OpenFile(relativePath)|从目录中打开现有文件进行读取。|


## <a name="object-properties"></a>对象属性
|名称|描述|
|--- |--- |
|文件|一个[集合](dbgmodel-namespace-collections.md)的[文件](dbgmodel-object-file.md)目录中。|
|SubDirectories|一个[集合](dbgmodel-namespace-collections.md)的[directory](dbgmodel-object-directory.md)目录中。|