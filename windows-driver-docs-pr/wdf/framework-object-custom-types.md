---
title: 框架对象自定义类型
description: 框架对象自定义类型
ms.assetid: E00393ED-7285-4354-9E1B-D9ABDB7DC9F2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c32d06367a86a3d27561afb28a368803abab664
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382868"
---
# <a name="framework-object-custom-types"></a>框架对象自定义类型


从 KMDF 1.11 版开始，该框架支持自定义的类型名称。 自定义的类型名称是一个字符串，该驱动程序可以将与 WDFOBJECT 实例相关联。 驱动程序定义其自己的自定义类型名称。 驱动程序已调用对象的创建方法后，驱动程序将指定对象的自定义类型名称。

使用这些宏来操作自定义的类型名称：

-   若要定义自定义的类型名称，请调用[ **WDF\_DECLARE\_自定义\_类型**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-declare-custom-type)从声明全局数据，例如标头文件的驱动程序的区域。
-   调用[ **WdfObjectAddCustomType** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectaddcustomtype)或[ **WdfObjectAddCustomTypeWithData** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectaddcustomtypewithdata)能够 framework 对象相关联的自定义类型。
-   调用[ **WdfObjectIsCustomType** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectiscustomtype)来确定的指定自定义类型是否为指定的对象。
-   在调用[ **WdfObjectAddCustomTypeWithData**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectaddcustomtypewithdata)，该驱动程序可以稍后调用[ **WdfObjectGetCustomTypeData** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectgetcustomtypedata)检索数据。

驱动程序可以将多个自定义的类型与单一框架对象相关联。 驱动程序还可以将多个框架对象关联的单个自定义类型。

在输出中 KMDF 调试器扩展，以及其他 WDF 对象信息显示自定义的类型名称。

```cpp
WDF_Object_Name, [custom_Type1_Name, custom_Type2_Name]
```

 

 





