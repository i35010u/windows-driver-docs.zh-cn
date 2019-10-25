---
title: 设计微型端口回调例程来处理 WMI 类
description: 设计可以通过数据字段处理 WMI 类的微型端口驱动程序回调例程
ms.assetid: 6e08f9c1-e541-4e5f-8c99-f81d5793cc21
keywords:
- WMI SRBs WDK 存储，设计回调例程
- 回调例程 WDK WMI SRBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d94ed37757124a85364223668781a085850e013
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845185"
---
# <a name="designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-with-data-fields"></a>设计可以通过数据字段处理 WMI 类的微型端口驱动程序回调例程


## <span id="ddk_designing_a_miniport_driver_callback_routine_that_handles_wmi_clas"></span><span id="DDK_DESIGNING_A_MINIPORT_DRIVER_CALLBACK_ROUTINE_THAT_HANDLES_WMI_CLAS"></span>


本部分说明回调例程如何处理包含数据字段的 WMI 类的输入和输出数据。

如果 WMI 类包含数据字段，则 WMI 工具套件将为数据生成结构声明。 结构声明与为保存属于类的 WMI 方法的输入和输出参数而生成的任何结构分离。 有关 WMI 工具套件生成的用于处理 WMI 方法的结构的详细信息，请参阅设计使用方法处理 WMI 类的微型端口驱动程序回调例程。

例如，假设我们使用**mofcomp.exe**编译以下 WMI 类定义，并使用**wmimofck**生成 .h 文件。

```cpp
class HBAFCPBindingEntry
{
  [HBAType("HBA_FCPBINDINGTYPE"),
   Values{"TO_D_ID", "TO_WWN", "TO_OTHER"},
   ValueMap{"0", "1", "2"},
   WmiDataId(1)
  ]
  uint32  Type;
  [HBAType("HBA_FCID"),
   WmiDataId(2)
  ]
  HBAFCPID  FCPId;
  [HBAType("HBA_FCPSCSIENTRY"),
   WmiDataId(3)
  ]
  HBAScsiID  ScsiId;
};
```

生成的 .h 文件将包含以下结构声明。

```cpp
typedef struct _HBAFCPBindingEntry
{
  ULONG  Type;
  HBAFCPID  FCPId;
  HBAScsiID  ScsiId;
} HBAFCPBindingEntry, *PHBAFCPBindingEntry;
```

在管理输入和输出数据时，可以将此结构声明转换为 SRB 的输入和输出缓冲区。

在返回之前，回调例程应调用[**ScsiPortWmiPostProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)。 此 SCSI 端口 WMI 库例程用信息更新请求上下文，例如请求的状态和返回数据的大小。 有关存储在请求上下文中的数据的详细信息，请参阅[**SCSIWMI\_request\_context**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmi_request_context)。

 

 




