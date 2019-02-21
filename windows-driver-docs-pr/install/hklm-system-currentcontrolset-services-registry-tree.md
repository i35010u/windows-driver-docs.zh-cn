---
title: HKLM\SYSTEM\CurrentControlSet\Services Registry Tree
description: HKLM\SYSTEM\CurrentControlSet\Services 注册表树将有关每个服务的信息存储在系统上。
ms.assetid: c966b029-8171-4db7-9fbb-3a4222ff184b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a705e118b4863cf39610a5baf8415fbf0b161c1d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545219"
---
# <a name="hklmsystemcurrentcontrolsetservices-registry-tree"></a>HKLM\\SYSTEM\\CurrentControlSet\\Services Registry Tree





**HKLM\\系统\\CurrentControlSet\\Services**注册表树将有关每个服务的信息存储在系统上。 每个驱动程序都有一个键的窗体**HKLM\\系统\\CurrentControlSet\\Services\\**<em>DriverName</em>。 PnP 管理器将传递此路径中的驱动程序*RegistryPath*参数时，它调用的驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。 驱动程序可以将在其项下的全局驱动程序定义数据存储**Services**树。 在初始化期间向驱动程序提供了此项下存储的信息。

以下键和值项属于特定的感兴趣：

<a href="" id="imagepath"></a>**ImagePath**  
值项，指定驱动程序的图像文件的完全限定的路径。 Windows 使用所需的创建该值**ServiceBinary**驱动程序的 INF 文件中的条目。 此条目是在*服务安装部分*由驱动程序的引用[ **INF AddService 指令**](inf-addservice-directive.md)。 此路径的典型值为 *%systemroot%*\\*system32\\驱动程序\\DriverName*.sys，其中*DriverName*是驱动程序的名称**Services**密钥。

<a href="" id="parameters"></a>**参数**  
一个用于存储特定于驱动程序的数据的键。 对于某些类型的驱动程序，系统需要查找特定值的条目。 可以将值项添加到使用此子项**AddReg**驱动程序的 INF 文件中的条目。

<a href="" id="performance"></a>**性能**  
一个指定可选的性能监视的信息的键。 此项下的值指定该 DLL 中的驱动程序的性能 DLL 的名称和某些导出函数的名称。 可以将值项添加到使用此子项**AddReg**驱动程序的 INF 文件中的条目。

 

 





