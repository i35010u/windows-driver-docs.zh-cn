---
title: 处理存储器微型端口驱动程序中的 WMI SRB
description: 处理存储器微型端口驱动程序中的 WMI SRB
ms.assetid: 92b78611-7e6f-4d77-9133-635df96584f0
keywords:
- 存储微型端口驱动程序 WDK，WMI Srb
- 微型端口驱动程序 WDK 存储，WMI Srb
- 有关 WMI Srb WMI Srb WDK 存储
- WMI Srb WDK 存储
- SRB WMI 支持 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fde44f7cd85051cd993054daa3bb3629508af880
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383110"
---
# <a name="handling-wmi-srbs-in-storage-miniport-drivers"></a>处理存储器微型端口驱动程序中的 WMI SRB


## <span id="ddk_handling_wmi_srbs_in_storage_miniport_drivers_kg"></span><span id="DDK_HANDLING_WMI_SRBS_IN_STORAGE_MINIPORT_DRIVERS_KG"></span>


WMI 接口有关主机总线适配器 (HBA)，该报表信息或允许 WMI 客户端与 HBA 的存储微型端口驱动程序进行交互，通常需要的微型端口驱动程序可以作为 WMI 提供程序。 存储微型端口驱动程序将注册为 WMI 提供程序后，它必须准备好处理一种特殊的 SCSI 请求块 (SRB) 调用 Windows Management Instrumentation (WMI) SCSI 请求块 ([**SCSI\_WMI\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff565397))。

若要准备存储微型端口驱动程序来处理 WMI Srb，完成以下步骤：

1.  设计和编译托管对象格式 (MOF) 文件，描述由系统提供的 MOF 文件未定义的 WMI 架构那些部分。

    MOF 语法的说明，请参阅[WMI 数据和事件块的 MOF 语法](https://msdn.microsoft.com/library/windows/hardware/ff556400)。

2.  实现微型端口驱动程序回调例程。

    SCSI 端口 WMI 库简化了处理 WMI Srb 微型端口驱动程序。 若要使用 SCSI 端口 WMI 库，实现*HwScsiWmiXxx*中所述的回调例程[SCSI 微型端口驱动程序例程](https://msdn.microsoft.com/library/windows/hardware/ff565312)。

3.  将所需的代码添加到微型端口驱动程序[ **DriverEntry 的 SCSI 微型端口驱动程序**](https://msdn.microsoft.com/library/windows/hardware/ff552654)例程。

4.  将所需的代码添加到微型端口驱动程序[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)例程。

5.  将所需的代码添加到微型端口驱动程序[ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)例程。

有关实现的上一步骤的信息，请参阅在本部分中所包含的以下主题：

[端口驱动程序如何处理 WMI 请求](how-the-port-driver-processes-wmi-requests.md)

[使用 SCSI 端口 WMI 库](using-the-scsi-port-wmi-library.md)

[设计 WMI 微型端口驱动程序回调例程](designing-wmi-miniport-driver-callback-routines.md)

[修改存储微型端口驱动程序例程以支持 WMI Srb](modifying-storage-miniport-driver-routines-to-support-wmi-srbs.md)

 

 




