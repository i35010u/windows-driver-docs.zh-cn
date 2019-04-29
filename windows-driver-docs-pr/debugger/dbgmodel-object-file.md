---
title: 调试器数据模型 - 文件对象
description: 文件对象用于打开、 编辑和其他操作在文件系统上的文件。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: eb3f164e08775bfac769ba0edfd24f5056c2748d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376085"
---
# <a name="file-objects"></a>File 对象 
## <a name="summary"></a>总结
文件对象用于打开、 编辑和其他操作在文件系统上的文件。

## <a name="object-methods"></a>对象方法
|名称|返回类型|签名|描述|
|--- |--- |--- |--- |
|关闭||Close （)|关闭该文件。 |
|DELETE||Delete （)|删除文件|
|打开||Open(disposition)|打开该文件与给定*处置*。 *处置*可能是"OpenExisting"、"CreateNew"或"CreateAlways"之一。|
|ReadBytes|字节数组|ReadBytes(byteCount)|从文件中读取指定的字节数，并返回一个可索引且可迭代这些字节数组。|
|WriteBytes||WriteBytes(bytes, [byteCount])|将指定的字节写入到文件。 如果*byteCount*未提供，可以循环访问的每个字节*字节*写入文件; 否则为第一个*byteCount*内的字节*字节*写入。|

## <a name="object-properties"></a>对象属性
|名称|描述|
|--- |--- |
|扩展|包含文件扩展名的字符串。|
|名称|包含的文件的名称的字符串。|
|路径|包含文件的完全限定的路径的字符串。|
|位置|在文件中的当前读/写光标的位置。|
|大小|文件的大小（以字节为单位）。|

## <a name="remarks"></a>备注
如果要从 JavaScript 脚本如垃圾收集环境使用这些文件，它们应关闭时不能再在中使用，而无需等待垃圾回收会导致要关闭的文件。
