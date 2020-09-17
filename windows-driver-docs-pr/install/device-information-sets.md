---
title: 设备信息集
description: 设备信息集
ms.assetid: 20539c63-10b1-408a-8c60-da444f54b64e
keywords:
- 设备信息元素 WDK 设备安装
- 设备信息设置 WDK 设备安装
- 信息集 WDK 设备
- 枚举设备信息 WDK
- SetupDiEnumDeviceInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abf15daf1df5c9e938a64877f5caabd0a9205c18
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715604"
---
# <a name="device-information-sets"></a>设备信息集

在用户模式下，属于[设备安装程序类](./overview-of-device-setup-classes.md)或[设备接口类](./overview-of-device-interface-classes.md)的设备使用*设备信息元素*和*设备信息集*进行管理。 设备信息集包含属于某些设备安装程序类或设备接口类的所有设备的设备信息元素。

每个设备信息元素都包含设备的 *devnode*的句柄，并包含指向与该元素描述的设备关联的所有设备接口的链接列表的指针。 如果设备信息集描述了安装类的成员，则该元素可能不指向任何设备接口，因为安装程序类成员不一定与接口相关联。

下图显示了设备信息集的内部结构。

![说明设备信息集的关系图](images/devinfosets.png)

## <a name="creating-a-device-information-set"></a>创建设备信息集

使用 [**SetupDiCreateDeviceInfoList**](/windows/win32/api/setupapi/nf-setupapi-setupdicreatedeviceinfolist)创建设备信息集后，可以使用 [**SetupDiCreateDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)一次创建一个设备信息元素并将其添加到列表中。 另外，也可以调用 [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw) 来创建设备信息集，该信息集由与指定设备安装程序类或设备接口类关联的所有设备组成。

## <a name="enumerating-device-information"></a>枚举设备信息

一旦创建了设备信息集，就可以枚举属于该集的设备和设备接口，但每个枚举类型都需要不同的操作。 [**SetupDiEnumDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinfo) 枚举属于满足特定条件的信息集的所有设备。 对 **SetupDiEnumDeviceInfo** 的每次调用都会提取大致对应于设备信息元素的 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构。 SP_DEVINFO_DATA 包含设备所属的类的 GUID 和指向设备的 devnode 的 *设备实例* 句柄。 SP_DEVINFO_DATA 结构和完整设备元素之间的主要区别在于 SP_DEVINFO_DATA *不* 包含与设备关联的接口的链接列表。 因此，不能使用 **SetupDiEnumDeviceInfo** 来枚举设备信息集中的接口。

若要枚举设备信息集中的设备接口，请调用 [**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)。 此例程逐句通过设备信息集中的所有设备信息元素，在每个元素的接口列表中提取接口，并为每个调用返回一个接口。 如果将 SP_DEVINFO_DATA 结构作为其第二个参数中的输入传递 **，则它** 将枚举仅限制为与 SP_DEVINFO_DATA 指示的设备关联的接口。

**SetupDiEnumDeviceInterfaces** 返回 [**SP_DEVICE_INTERFACE_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_data) 结构。 SP_DEVICE_INTERFACE_DATA 包含接口类 GUID 和有关接口的其他信息，包括包含编码信息的保留字段，该字段可用于获取接口的名称。 若要获取接口名称，需要执行一个额外步骤：必须调用 [**SetupDiGetDeviceInterfaceDetail**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila) 。 **SetupDiGetDeviceInterfaceDetail** 返回 [**SP_DEVICE_INTERFACE_DETAIL_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_detail_data_a) 类型的结构，该结构包含用于定义接口的系统对象树中的路径。