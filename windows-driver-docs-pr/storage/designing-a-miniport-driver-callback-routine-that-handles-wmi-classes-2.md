---
title: 设计微型端口驱动程序回调例程来处理 WMI 类
description: 设计可以通过方法处理 WMI 类的微型端口驱动程序回调例程
keywords:
- WMI SRBs WDK 存储，设计回调例程
- 回调例程 WDK WMI SRBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53f42c40e574dc8fe449c318f793c9b853c3680b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835345"
---
# <a name="designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-with-methods"></a>设计可以通过方法处理 WMI 类的微型端口驱动程序回调例程


## <span id="ddk_designing_a_miniport_driver_callback_routine_that_handles_wmi_clas"></span><span id="DDK_DESIGNING_A_MINIPORT_DRIVER_CALLBACK_ROUTINE_THAT_HANDLES_WMI_CLAS"></span>


本部分使用包含 WMI 方法的示例 WMI 类，并说明相应的微型端口驱动程序回调例程的外观。 有关执行 WMI 方法的微型端口驱动程序回调例程的详细信息，请参阅 [**HwScsiWmiExecuteMethod**](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)。

以下示例 WMI 类包含 WMI 方法：

```cpp
class MSFC_HBAAdapterMethods
{
    [key] 
    string InstanceName;
    boolean Active;
    [
     Implemented,
     WmiMethodId(1)
    ]
    void GetDiscoveredPortAttributes(
            [in ] uint32 PortIndex,
            [in ] uint32 DiscoveredPortIndex,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
            [out, HBAType("HBA_PORTATTRIBUTES") ] 
                MSFC_HBAPortAttributesResults PortAttributes
            );
    [
     Implemented,
     WmiMethodId(2)
    ]
    void GetPortAttributesByWWN(
            [in, HBAType("HBA_WWN")] uint8 wwn[8],
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
          [out, HBAType("HBA_PORTATTRIBUTES") ] 
                MSFC_HBAPortAttributesResults PortAttributes
            );
};
class MSFC_HBAFCPInfo
{
    [key] 
    string InstanceName;
    boolean Active;
    [
     Implemented,
     WmiMethodId(1)
    ]
    void GetFcpTargetMapping(
            [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
            [in ] uint32 InEntryCount,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
            [out] uint32 TotalEntryCount,
            [out] uint32 OutEntryCount,
            [out, WmiSizeIs("OutEntryCount")] HBAFCPScsiEntry  
                 Entry[]
            );
};
```

**MSFC \_ HBAAdapterMethods** 类包含两个 **GetDiscoveredPortAttributes** 和 **GetPortAttributesByWWN** 方法。 MSFC \_ HBAFCPInfo 类包含 **GetFcpTargetMapping** 中的一种方法。

当 SCSI 端口 WMI 库调度例程调用微型端口驱动程序的 execute 方法回调例程时，它将传入一个 *GuidIndex* 值，该值标识 WMI 类、标识类中方法的 *MethodId* 值和一个 *InstanceIndex* 值，用于标识要处理的类的多个实例。 对于任何给定的类、方法和类实例组合，回调例程应采取相应的操作。

下面的示例演示 execute 方法回调例程如何处理上一示例中的方法。

```cpp
HwScsiWmiExecuteMethod (
    IN PVOID Context,
    IN PSCSIWMI_REQUEST_CONTEXT DispatchContext,
    IN ULONG GuidIndex,
    IN ULONG InstanceIndex,
    IN ULONG MethodId,
    IN ULONG InBufferSize,
    IN ULONG OutBufferSize,
    IN OUT PUCHAR Buffer
    )

  switch(GuidIndex) { 
    case MSFC_HBAAdapterMethodsGuidIndex:
    {
      switch(MethodId) {
      case GetDiscoveredPortAttributes:
        // handle method here 
        Switch(InstanceIndex) {
        case 1:
          // handle instance 1
          PGetDiscoveredPortAttributes_IN In;
          PGetDiscoveredPortAttributes_OUT Out;
          // note: input and output parameters use the same buffer
          In = (PGetDiscoveredPortAttributes_IN)Buffer;
          Out = (PGetDiscoveredPortAttributes_OUT)Buffer;
          // put code for method here
          break;
        case 2:
       // handle instance 2
        default:
          break;
        }
      case GetPortAttributesByWWN:
        // handle method here 
      default:
        break;
    }
    case MSFC_HBAFCPInfoGuidIndex:
    {
      switch(MethodId) {
      case GetFcpTargetMapping:
        // handle method here 
      default:
        break;
      }
    }
```

WMI 工具套件 (**mofcomp.exe** 和 **wmimofck**) 通过自动生成二进制类型库和标头文件（为每个 WMI 类 GUID 索引和每个方法标识符定义一个符号常量）简化了写入此例程的任务。 有关如何使用这些工具的详细信息，请参阅 [编译驱动程序的 MOF 文件](../kernel/compiling-a-driver-s-mof-file.md) 和 [使用 wmimofck.exe](../kernel/using-wmimofck-exe.md)。

**Wmimofck** 工具从 **mofcomp.exe** 生成的 bmf 二进制文件生成 .h 文件。 它通过将后缀 "GuidIndex" 连接到 WMI 类的名称，形成类索引的符号常数的名称。 例如，使用 **MSFC \_ FibrePortHBAMethods** 类时，该工具会创建一个名为 **MSFC \_ FibrePortHBAMethodsGuidIndex** 的符号常量，表示该类的 GUID 索引。 与此类似，该工具将使用方法名称来形成表示方法的符号常数，但不添加任何后缀。 方法的符号常数的名称只是方法的名称。 在此示例中，switch 语句测试方法标识符的值。 Switch 语句中的每个用例都对应于一个方法名称。

用于定义 WMI 类方法的 MOF 语法类似于例程;但是，WMI 方法不是例程。 当 **mofcomp.exe** 和 **WMIMOFCK** 工具处理 MOF 文件中的方法定义时，它们将为方法生成两个单独的 C 语言结构声明。 一个结构是在 MOF 文件中通过 "in" 前缀标识的参数，另一个是 \[ " \] \[ out" 前缀标识为输出参数的参数的另一个结构 \] 。

**Wmimofck** 工具通过将 "IN" 的后缀连接到方法的名称，形成包含方法的输入参数的结构的名称 \_ 。 例如，如果方法的名称为 **GetDiscoveredPortAttributes**，则 **wmimofck** 将自动为中名为 GetDiscoveredPortAttributes 的结构生成声明 \_ 。 同样， **wmimofck** 为名为 GetDiscoveredPortAttributes 的结构生成一个声明 \_ ，该结构包含方法的输出参数。

下面的代码片段演示了 execute 方法回调例程如何在名为 **MSFC \_ HBAPortMethods** 的类中验证名为 **GetDiscoveredPortAttributes** 的方法的输入和输出缓冲区的大小：

```cpp
case MSFC_HBAPortMethodsGuidIndex:
  switch(MethodId) {
    case GetDiscoveredPortAttributes:
  {
      BOOLEAN bInputBigEnough = (InBufferSize >= 
              sizeof(GetDiscoveredPortAttributes_IN))
      BOOLEAN bOutputBigEnough = (OutBufferSize >= 
              sizeof(GetDiscoveredPortAttributes_OUT))
      if (bInputBigEnough && bOutputBigEngough) {
        PGetDiscoveredPortAttributes_IN In;
        PGetDiscoveredPortAttributes_OUT Out;

        In = (PGetDiscoveredPortAttributes_IN)Buffer;
         Out = (PGetDiscoveredPortAttributes_OUT)Buffer;
        // 
        // process method here
      //
        status = SRB_STATUS_SUCCESS;
      } else {
        status = SRB_STATUS_DATA_OVERRUN;
      }
    }
```

在返回之前，回调例程应调用 [**ScsiPortWmiPostProcess**](/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)。 此 SCSI 端口 WMI 库例程用信息更新请求上下文，例如请求的状态和返回数据的大小。 有关存储在请求上下文中的信息的详细信息，请参阅 [**SCSIWMI \_ 请求 \_ 上下文**](/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmi_request_context)。

 

