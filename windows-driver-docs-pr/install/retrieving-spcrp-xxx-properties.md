---
title: 检索 SPCRP_Xxx 属性
description: 检索 SPCRP_Xxx 属性
ms.assetid: a5d52da9-a593-42bd-aeaf-8ab203bc3d21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd557f70585b4b3903503d170c39f80621526140
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382278"
---
# <a name="retrieving-spcrpxxx-properties"></a>检索 SPCRP_Xxx 属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)支持的设备实例属性中定义的 SPCRP_Xxx 标识符对应*Setupapi.h*. 这些属性描述的特征[设备安装程序类](device-setup-classes.md)。 统一的设备属性模型使用[属性键](property-keys.md)来表示这些属性。

Windows Server 2003、 Windows XP 和 Windows 2000 还支持大部分设备安装程序类属性。 但是，这些早期版本的 Windows 不支持统一的设备属性模型属性键。 相反，这些版本的 Windows 版本使用 SPCRP_*Xxx*标识符表示并访问设备安装程序类属性。 若要保持与早期版本的 Windows 兼容性，Windows Vista 和更高版本还支持使用 SPCRP_*Xxx*标识符，以访问设备安装程序类属性。 但是，应使用统一的设备属性模型属性键来访问设备安装程序类属性。

系统定义的设备安装程序类属性的列表，请参阅[设备安装程序类属性，对应于 SPCRP_Xxx 标识符](https://docs.microsoft.com/previous-versions/ff542245(v=vs.85))。 属性的密钥标识符用于访问在 Windows Vista 和更高版本中的属性按列出的设备安装程序类属性。 与属性键一起提供的信息还包括相应 SPCRP_*Xxx*可用于访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的属性的标识符。

有关如何使用属性键来访问在 Windows Vista 和更高版本的设备安装程序类属性的信息，请参阅[访问设备类属性 （Windows Vista 和更高版本）](accessing-device-class-properties--windows-vista-and-later-.md)。

若要检索在 Windows Server 2003、 Windows XP 和 Windows 2000 上的设备安装程序类属性，请使用[ **SetupDiGetClassRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)函数。

若要使用 SetupDiGetClassRegistryProperty 检索与 SPCRP_Xxx 标识符相对应的属性，请按照下列步骤：

1.  调用**SetupDiGetClassRegistryProperty**并提供以下参数值：

    -   设置*ClassGuid*为指向表示要为其检索属性的设备安装程序类的 GUID。
    -   设置*属性*到带前缀"SPCRP_"的属性标识符为其检索属性值的大小。
    -   设置*PropertyRegDataType*到**NULL**。
    -   设置*PropertyBuffer*到**NULL**。
    -   设置*PropertyBufferSize*为零。
    -   设置*RequiredSize*到指向 DWORD 类型的变量接收大小，以字节为单位的所请求的属性。
    -   设置*MachineName*到的计算机的名称。
    -   设置为保留**NULL**。

    以响应对的调用[ **SetupDiGetClassRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)， **SetupDiGetClassRegistryProperty**设置\* *RequiredSize*大小，以字节为单位，检索属性值，所需的缓冲区的记录的错误代码 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 随后调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回最近记录的错误代码。

2.  调用**SetupDiGetClassRegistryProperty**再次以检索属性值，并提供相同的第一个调用中，除以下更改外中提供的参数：
    -   设置*PropertyBuffer*到指向该缓冲区用于接收的属性值的指针。
    -   设置*PropertyBufferSize*到的大小，以字节为单位的*PropertyBuffer*缓冲区。 首次调用**SetupDiGetClassRegistryProperty**检索所需的大小*PropertyBuffer*中的缓冲区\* *RequiredSize*。

如果第二个调用**SetupDiGetClassRegistryProperty**成功， **SetupDiGetClassRegistryProperty**设置\* *PropertyRegDataType*到注册表数据类型，设置*PropertyBuffer*属性值设置到缓冲区\* *PropertyBufferSize*大小，以字节为单位，属性值，并返回**TRUE**。 如果函数调用失败， **SetupDiGetClassRegistryProperty**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

 

 





